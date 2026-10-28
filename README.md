# Toml encoder

Minimal toml encoder written in Odin, using it's type reflection system.

Only supports strings, integers, floats, booleans, inline structs/tables and static arrays for now.

Only for Toml 1.1.0 as earlier versions didn't support newlines in inline tables.

Full spec compatibility isn't to be expected, but should work for simple structs.

## Usage

Basically make a string builder and pass it along with your Odin struct to `write_value` function.

```odin
import "toml"

State :: struct {
	background: distinct [4]u8,
	vsync: bool,
	fullscreen: bool,
	resizable: bool,
  positions: struct {
    Farm: [2]f32,
    Fish: [2]f32,
    Pig: [2]f32,
    Goat: [2]f32,
    Hen: [2]f32,
    Sheep: [2]f32,
    Cow: [2]f32
  }
}

state := State{
  background = [4]u8{96, 186, 74, 255},
  vsync = true,
  fullscreen = false,
  resizable = true,
  positions = {
    Farm = [2]f32{35, 600},
    Fish = [2]f32{210, 82},
    Pig = [2]f32{256, 229},
    Goat = [2]f32{454, 279},
    Hen = [2]f32{48, 153},
    Sheep = [2]f32{73, 43},
    Cow = [2]f32{367, 32}
  }
}

sb, alloc_err := strings.builder_make()
if (alloc_err != nil) { return } // string builder allocation can fail

toml.write_value(&sb, state^)
```

## Inspiration

The defacto [library implementation](https://github.com/Up05/toml_parser) of reflective Toml parsing in Odin\
[A way to implement minimal reflective JSON encoding in Odin](https://youtu.be/YyvGVy-IqYA)

## License

This project is dedicated to public domain. See [LICENSE](./UNLICENSE) for more details.
