# Sinatra Nested Forms

## Notes

In web apps, we use forms to create objects. Nested forms create multiple objects.

### The Models

- To create two different classes of objects, we need to create two models.
  - Example: When registering students for a new school year and assigning them their schedules, we would make `Student` and `Course` classes.

### Creating the Form

- With nested forms, we need to restructure our `params` hash to have nested hashes.
- ERB handles the first level of nesting, so instead of having to do `params["student"] = {}`, we can just go straight into the `student` hash. ERB assumes that the name of your top-level hash is the first key, so the code to call the value associated with the nested "name" key would be `student["name"]`.
  - This also applies to the HTML for a form where you'll use `student[name]` as the `name` attribute of the `input` tag. For our nested `course` objects, use `student[course][name]` and `student[course][topic]`.
- To allow for multiple courses, the `courses` key should store an array of nested hashes.
  - For this case, in our HTML form we'll use `student[courses][][name]` and `student[courses][][topic]` as the `name` attribute of the `input` tag.

### The Display View

- In the view, we use the instance variable `@student` and the reader methods `.name` and `.grade` to display the student's information.
- We then iterate over `@courses` to display the name and topic of each course.

### The Controller

- We need two controller actions: one to serve up the form and one to process the data from the form.

## Code Examples

### Student Class

```ruby
class Student
  attr_reader :name, :grade
  
  STUDENTS = []
  
  def initialize(params)
    @name = params[:name]
    @grade = params[:grade]
    STUDENTS << self
  end
  
  def self.all
    STUDENTS
  end
  
end
```

### Course Class

```ruby
def Course
  attr_reader :name, :topic
  
  COURSES = []
  
  def initialize(args)
    @name = args[:name]
    @topic = args[:topic]
    COURSES << self
  end
  
  def self.all
    COURSES
  end
  
end
```

### Nested Params Hash

```ruby
params = {
  "student" => {
    "name" => "Vic",
    "grade" => "12",
    "courses" => [
      {
        "name" => "AP US History",
        "topic" => "History"
      },
      {
        "name" => "AP Human Geography",
        "topic" => "History"
      }
    ]
  }
}

# In this hash, both `student` and `course` can have the key `name` because they're in different namespaces.
```