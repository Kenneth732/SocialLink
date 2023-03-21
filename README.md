# README

This README would normally document whatever steps are necessary to get the
application up and running.

Things you may want to cover:

* Ruby version

* System dependencies

* Configuration

* Database creation

* Database initialization

* How to run the test suite

* Services (job queues, cache servers, search engines, etc.)

* Deployment instructions

* ...


# Create a new Ruby on Rails application: In the terminal, navigate to the directory where you want to create your application and run the following command:

```
rails new my_app_name
```

# Generate the models: Run the following commands in the terminal to generate the User, Contact, Message, Like, and Profile models:

```
rails generate model User name:string email:string password_digest:string
rails generate model Contact name:string email:string user:references
rails generate model Message content:text user:references contact:references
rails generate model Like user:references message:references
rails generate model Profile bio:text user:references
```

This will create the following models with their respective attributes:

User: name, email, password_digest
Contact: name, email, user_id
Message: content, user_id, contact_id
Like: user_id, message_id
Profile: bio, user_id
# Define the associations in the models: Open each model file (user.rb, contact.rb, message.rb, like.rb, profile.rb) and add the following associations:


```
class User < ApplicationRecord
  has_many :contacts
  has_many :messages
  has_many :likes
  has_one :profile
end
```

```
class Contact < ApplicationRecord
  belongs_to :user
  has_many :messages
end
```

```
class Message < ApplicationRecord
  belongs_to :user
  belongs_to :contact
  has_many :likes
end
```
```
class Like < ApplicationRecord
  belongs_to :user
  belongs_to :message
end
```

```
class Profile < ApplicationRecord
  belongs_to :user
end
```
# These associations define the relationships between the models:

A User has many Contacts, Messages, and Likes, and has one Profile.
A Contact belongs to a User and has many Messages.
A Message belongs to a User and a Contact, and has many Likes.
A Like belongs to a User and a Message.
A Profile belongs to a User.

# Create the database tables: In the terminal, run the following command to create the database tables:

```
rails db:migrate
```
This will create the necessary tables in the database based on the models you've defined.

# Define the model attributes and validations: In each model, define the attributes that you want to store in the database and any validations that you want to add to those attributes. Here's an example for the Contact model:

```
class Contact < ApplicationRecord
  belongs_to :user
  has_many :messages

  validates :name, presence: true
  validates :email, presence: true, uniqueness: { scope: :user_id }
end
```
This defines the following attributes and validations:

A Contact belongs to a User and has many Messages.
A Contact has a name attribute that must be present.
A Contact has an email attribute that must be present and unique within the scope of the user.
You would define the attributes and validations in the other models similarly.

# Define any necessary controllers and views: Depending on your application, you may need to define controllers and views to handle user



