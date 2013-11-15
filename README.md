# Livid Mode

This is just a mode built on top of
[skewer-mode](https://github.com/skeeto/skewer-mode) to emulate the
functionality of browser-based HTML/JS/CSS editors who automatically
evaluate code on every change.

Whereas skewer allows you to evaluate the buffer or individual forms
with commands/key-bindings, this **just f'ing does it** for you. What
could be _angrier_ than that?

However, code is **not** evaluated every single time the buffer changes. Here's
what happens whenever Emacs runs its `after-changed-functions` hook:

1. First, livid-mode can be paused. If it has been, nothing happens.
2. Then, the trimmed contents are compared to the previously evaluated
contents. If they're the same, nothing happens.
3. Next, syntax is checked by the external `js` command. If there is
any SyntaxError, nothing happens. (You can override this behavior if
you want via `(setq livid-validate-javascript nil)`.)
4. Finally, skewer sends the buffer's code to be evaluated in the
browser, asynchronously. (This is presumably all about the side
effects, so return values disappear into the ether.)

## Installation

### Package

It's in marmalade, called `livid-mode`.

### Manual

Clone the repo, stick it in .emacs.d or wherever, and `(require 'livid-mode)`.

## Usage

Just do M-x livid-mode on any js2-mode buffer. The mode will initiate
skewer-mode if it is not present, but assumes you already have the
simple-httpd server running.

At that point, have a web browser loaded to a page with this script tag present
(adjusted to correspond with the host/port you're using), as per usual
with skewer:

```
<script src="http://localhost:8080/skewer"></script>
```

## License

Public domain, like skewer-mode.
