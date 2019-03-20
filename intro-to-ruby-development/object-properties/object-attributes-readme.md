# Object Attributes Readme

- Reader methods (or "getters") return information stored in an instance variable.
- Writer methods (or "setters") makes an attribute writable.
  - The setter method is defined with an `=`, equals sign, appended to the name of the method. The `=` is followed by the `(argument_name)`.
- The call a setter method, you use dot notation to call the method and set it equal to a new value.
- In Ruby, it is possible to set an instance variable with the following method: `object.instance_variable_set(:instance_variable, "value")`
- It is also possible to retrieve an instance variable from an object with the following method: `object.instance_variable_get(:instance_variable) => "value"`
  - This is syntactic vinegar and not flexible and should not be used