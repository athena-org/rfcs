- Feature Name: add_text_support_to_phosphorus
- Affected Projects: Phosphorus, Any Phosphorus Users
- Start Date: 2015-05-07
- RFC PR: athena-org/rfcs#1

# Summary

Add support for rendering text to Phosphorus. As well, add a Text and TextBox widget.

# Motivation

Phosphorus to be useful as a UI library should be able to render text output and receive text input.

# Detailed design

For text rendering, gfx_text should be used. If gfx_text misses any functionality we need, it should added. This library is not part of the Athena project, but it is permissively licensed and accepts pull requests. Gfx_text uses freetype for actual font rendering, which means we will also be depending on freetype.

After text rendering has been added, the following widgets should be added to the default set:
- [ ] Text
    - [x] Displays text on the screen.
    - [ ] Text can be set before first rendering and changed on the fly.
- [ ] TextBox
    - [ ] Displays text on the screen as typed by the user.
    - [ ] A default can be set and the value can be changed by code at any time.

# Drawbacks

There's no reason this feature should not be added. It's a crucial feature of any UI library. The freetype dependency however might be tricky. It's preferential to avoid any C dependencies as anything written in pure rust will work better cross platform.

# Alternatives

An alternative to the freetype dependency would be to use a pure rust alternative. None of those exist at the time of writing, so a new one would have to be made. This would require a lot of work and probably last longer than the current scope of the project.

# Unresolved questions

No unresolved questions at this time.
