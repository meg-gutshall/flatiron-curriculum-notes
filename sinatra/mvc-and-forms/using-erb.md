# Lesson: Using ERB

## Notes

Most major web frameworks provide some means of view templating (i.e. allowing the view, in our case an HTML document, to be constructed using a combination of HTML and Ruby).

### Embedding Ruby

ERB and other templating engines allow us to modify the content and structure of our HTML code. With ERB, we do this using two different types of tags: the substitution tag (`<%=`) and the scripting tag (`<%`).

#### Substitution Tags

The substitution tag evaluates Ruby code and then displays the results into the view. It opens with `<%=` and closes with `%>`. Inside of these tags, you can write any valid Ruby code that you want.

#### Scripting Tags

Scripting tags open with `<%` and close with `%>`. They evaluate-but do not actually display-Ruby code.

#### Iteration

We can also use iteration to manage lists of items. We use the substitution tag to display the value of the inner variable being iterated upon.