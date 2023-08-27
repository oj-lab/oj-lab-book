# Model Design Rules

🎯 You should design your model first before providing any kind of service.

Briefly speeking,
OJ Lab Service runs with models
which mainly shows in **JSON** and mapped by **GORM** in database.

## Usage of Struct Tag

To reduce the complexity of model usage,
we should design as fewer models as possible,
and the relationship between models should be well designed.

### Fields Control

In different situations,
the model will carry different fields.
(
    For example,
    the `password` field should be hidden in most cases,
    but it should be shown when creating a new user.
    Also,
    to avoid security problems,
    the `password` field will not saved directly to database,
    but a `hashed_password` field will be saved instead.
)

### Model Associations

The model may have associations with other models.
(
	For example,
	the `user` model may have a `role` field,
	which is a list of `role` model.
	Also,
	the `role` model may have a `user` field,
	which is a list of `user` model.
)
Usually, controlling these associations is very complex,
but we can rely on GORM to make it easier.

### Solutions

Thanks to the ability of struct tag in JSON and GORM,
we nearly don't need to write any model conversion codes.

The user struct is defined as below:

```go
type User struct {
	MetaFields
	Account        string  `gorm:"primaryKey" json:"account"`
	Name           string  `json:"name"`
	Password       *string `gorm:"-:all" json:"password,omitempty"`
	HashedPassword string  `gorm:"not null" json:"-"`
	Roles          []*Role `gorm:"many2many:user_roles;" json:"roles,omitempty"`
	Email          string  `gorm:"unique" json:"email,omitempty"`
	Mobile         string  `gorm:"unique" json:"mobile,omitempty"`
}

type Role struct {
	Name  string  `gorm:"primaryKey" json:"name"`
	Users []*User `gorm:"many2many:user_roles" json:"users,omitempty"`
}
```

You can try refering the following links to learn:

- [GORM Declaring Models](https://gorm.io/docs/models.html)
- [GORM Many To Many](https://gorm.io/docs/many_to_many.html)
- [Using JSON in Go](https://blog.logrocket.com/using-json-go-guide/)

> We don't get a very good JSON usage document for now.
> Simply search for 'go JSON struct tag' on the internet may help.

## Model Naming

The struct and field naming will effect the table naming for GORM.
Although GORM provides a way to customize table name,
but it can be really confuse when struct convert to structs and got different table names.

So it will be better to keep the default naming rules and make table and struct names the same.
Then we will get fewer struct being defined, and less conversion which may cause confusion.

Another thing which may cause confusion is when you are trying to define model like `Tag`, `Form` etc.
These names only describe the model itself,
but do not show any relationship between models,
also there are some other models with the same name (like there might be many `Tag` models).
So it will be better to add some prefix to the model name,
but don't use the parent model name as prefix (like `UserTag` or `ProblemTag`).
Try to be more specific for the real usage (like `AlgorithmTag`).
