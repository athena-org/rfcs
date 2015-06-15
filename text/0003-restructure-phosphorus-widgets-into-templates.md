- Feature Name: restructure_phosphorus_widgets_into_templates
- Affected Projects: Phosphorus, Any Phosphorus Users
- Start Date: 2015-05-27
- RFC PR: [athena-org/rfcs#3](https://github.com/athena-org/rfcs/pull/3)

# Summary

Replace the current widgets system in phosphorus with a template-based system.
This RPC is intentionally loosely defined as the API's far from stabilizing.

# Motivation

The current widget system works for static UIs but it quickly becomes unmanageable for UIs that have to change depending on user input. This problem already has surfaced in *athena_editor*.

# Detailed design

- Remove the `root` parameter in `Gui::new()` and the `root`, `root_mut` and `get_root` property accessors.
- Remove the current structure of assembling widgets with builders.
- Replace the widget structure with a template structure.
- Make Gui render an actual image using the template and controllers, updating as needed.

The following is a sample piece of code that shows how the Phosphorus API should be used after these changes:

```Rust
// # Code that does not require any gfx templates:

struct MyController {
    pub text_value: String
}

let template = TemplateElement::new("layout")
    .with_attr("style_size", "[600, 500]")
    .with_attr("style_background", "[21, 23, 24]")
    .with_child(TemplateElement::new("text").with_attr("value", "Hello world!"))
    .with_child(TemplateElement::new("let")
        .with_attr_bind("hello", "{new(\"HelloController\")}")
        .with_child(TemplateElement::new("text").with_attr_bind("value", "{hello.text}"))
    );


// # Code that requires gfx templates:

// Load the elements into a GUI
let gui = gui::new(&mut gfx_factory, template);

// Bind the controllers to their names
gui.register_controller("HelloController", || MyController { text_value: String::from("Test!") });

// Display the Gui
gui.draw(&mut gfx_stream);
```

# Drawbacks

This system is more complex to implement that the previous static widgets system.
The binding mini-language is a complex piece of the puzzle. It's likely we'll have
to delay it from being the main way to set bindings and use placeholder helpers
for now.

# Alternatives

Templating and controllers could be kept in a separate crate from Phosphorus, with
Phosphorus only having a very tiny widgets system. This however would make Phosphorus
lose focus.

# Unresolved questions

The binding system's API is still mostly undecided. As well, the mini-language used
for defining bindings isn't defined formally yet.
