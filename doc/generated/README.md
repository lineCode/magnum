Source files for images in Magnum documentation
-----------------------------------------------

Compile and install Magnum with `Sdl2Application`, windowless application for
your platform and `magnum-distancefieldconverter` utility and any `PngImporter`
and `PngImageConverter` plugins from Magnum Plugins.

Create build dir, point CMake to this directory and compile the executables:

    mkdir build-doc
    cd build-doc
    cmake ../doc/generated
    cmake --build .

### "Getting started" image

Displayed by the `hello` executable. Run the app and take screenshot using
KSnapshot (including decorations, 880x707). Similarly for the gray version. The
resulting files should be resized to half the size and without alpha channel
using imagemagick:

```bash
mogrify -flatten -background '#ffffff' -resize 440 getting-started.png
mogrify -flatten -background '#ffffff' -resize 440 getting-started-blue.png
```

The output printed by the application can be used to update the example output
in `doc/getting-started.dox`.

### Shader images

Generated by the `shaders` executable. Must be run in this directory, the
output is put into `doc/` directory. The executable requires two textures:

-   `vector.png`, generated as full-page PNG output at 90 DPI from `vector.svg`,
    converted to pure grayscale using imagemagick:

    ```bash
    mogrify -flatten -background '#ffffff' -format grayscale vector.png
    ```

-   `vector-distancefield.png`, generated as full-page PNG output at 360 DPI
    (1024x1024) and then processed through `magnum-distancefieldconverter`

    ```bash
    magnum-distancefieldconverter --importer PngImporter --converter PngImageConverter --output-size "64 64" --radius 16 vector-src.png vector-distancefield.png
    ```
