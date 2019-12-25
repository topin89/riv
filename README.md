# **Riv** the **R**ust **I**mage **V**iewer

Why riv? This project was born out of a frustration with image viewers on Mac. 
Generally the options are:-

* iPhoto - Way too heavy for just viewing images
* Preview - Clunky and really only good for viewing one image at a time
* Others that require a GUI folder browser

Riv on the other hand runs from the command line, and accepts a path with globs in quotes (with globstar `**` for recursive search). For example:-

```$ riv "**/*.jpg"```

## Manual

Start riv with 

```$ riv```. 

As an optional second parameter you can add a path with globs.

```$ riv "**/*.png"```

Without any second parameter, riv will look for all images in the current directory.

Set a destination folder for moving files with the `f` flag. The folder will be created if it doesn't exist.

```$ riv -f ~/saved_images```

Set a sorting order with the `s` or `--sort` flag, case insensitive.

```$ riv -s alphabetical "**/*.png"```

### Normal Mode Controls


| Key 1      | Key 2                      | Action                                              |
|------------|----------------------------|-----------------------------------------------------|
| 0-9 (many) | Key1 of action to perform  | Perform the specified action many times             |
| q          | Esc                        | Quit                                                |
| k/j        | Left/Right                 | Previous/Next Image                                 |
| i/o        | Up/Down                    | Zoom in/out                                         |
| r/R        |                            | Rotate image clockwise/counterclockwise             |
| H, J, K, L | Shift + Up/Down/Left/Right | Pan left/down/up/right                              |
| h          |                            | Flip image horizontally                             |
| v          |                            | Flip image vertically                               |
| b/w        | PageDown/PageUp            | Backward/Forward 10% of images                      |
| g/G        | Home/End                   | First/Last Image (55G jumps to the 55th image)      |
| m          |                            | Move image to destination folder (default ./keep)   |
| c          |                            | Copy image to destination folder (default ./keep)   |
| d          | Delete                     | Move image to OS specific trash location            |
| D          | Shift + Delete             | Delete image from its location                      |
| t          |                            | Toggle information bar                              |
| f          | F11                        | Toggle fullscreen mode                              |
| ?          |                            | Toggle help box                                     |
| z          | Left Click                 | Toggle actual size vs scaled image                  |
| Z          |                            | Center image                                        |
| . (period) |                            | Repeat last action                                  |


### Command Mode Controls


| Short | Long       | Argument | Action                              |
|-------|------------|----------|-------------------------------------|
| ng    | newglob    | Required | The new glob/directory/file         |
| ?     | help       | None     | Toggle help box                     |
| q     | quit       | None     | Quit                                |
|       | sort       | Optional | The method to sort by               |
| df    | destfolder | Required | New folder to move/copy images to   |
| m     | max        | Required | New maximum number of files to view |

### Sorting Options

| Option           | Description                                                                              |
|------------------|------------------------------------------------------------------------------------------|
| Alphabetical     | Alphabetically by filename only                                                          |
| Date             | By date last modified, most recent first                                                 |
| Size             | By size, largest first                                                                   |
| DepthFirst       | [Default] Ordered by farthest depth from current directory first                         |
| BreadthFirst     | Ordered by farthest depth from current directory last                                    |

Reverse the sorting order with `r` or `--reverse` flag

```$ riv -sr date **/*.png```

Set the maximum number of images to be displayed `m` or `--max` flag. 0 means infinitely many images.

```$ riv -m 0 **/*.png```


## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes.

### Prerequisites

You will need to install Rust and the SDL2 libraries to work with this project.

### Installing

Go [here](https://www.rust-lang.org/) for instructions on installing rust.
Go [here](https://github.com/Rust-SDL2/rust-sdl2) for instructions on installing SDL2.

You will also need sdl2_image and sdl2_ttf

#### Mac

The `trash` program is required for sending images to the trash.

`brew install trash sdl sdl2_image sdl2_ttf`

#### Arch

`sudo pacman -S sdl2 sdl2_image sdl2_ttf`

#### Ubuntu

`sudo apt-get install libsdl2-dev libsdl2-image-dev libsdl2-ttf-dev`

#### Other distros

Hopefully you can figure it out from the above instructions. If you do, please make a PR for this README with the specific instructions.

After that you can build with:

```cargo build```

#### Windows

Based in instructions from https://github.com/Rust-SDL2/rust-sdl2

1. Create the following folder structure in the same folder as your Cargo.toml:

   ```
   gnu-mingw\dll\32
   gnu-mingw\dll\64
   gnu-mingw\lib\32
   gnu-mingw\lib\64
   msvc\dll\32
   msvc\dll\64
   msvc\lib\32
   msvc\lib\64
   ```

   e.g with 

   ```
   mkdir gnu-mingw\dll\32
   mkdir gnu-mingw\dll\64
   mkdir gnu-mingw\lib\32
   mkdir gnu-mingw\lib\64
   mkdir msvc\dll\32
   mkdir msvc\dll\64
   mkdir msvc\lib\32
   mkdir msvc\lib\64
   ```

   

2. Download mingw and msvc development libraries from 

   - https://www.libsdl.org/download-2.0.php  (SDL2-devel-2.0.x-mingw.tar.gz & SDL2-devel-2.0.x-VC.zip)
   - https://www.libsdl.org/projects/SDL_image/  ( SDL2_image-devel-2.0.x-VC.zip & SDL2_image-devel-2.0.x-mingw.tar.gz )
   - https://www.libsdl.org/projects/SDL_ttf/ (SDL2_ttf-devel-2.0.x-VC.zip & SDL2_ttf-devel-2.0.x-mingw.tar.gz)

3. Unpack to folders of your choosing (You can delete it afterwards).

4. Copy the lib and dll files from the source archive to the directories we created in step 3 like so (you can skip targets you don't need):

```
SDL2-devel-2.0.x-mingw.tar.gz\SDL2-2.0.x\i686-w64-mingw32\bin 		-> 	gnu-mingw\dll\32
SDL2-devel-2.0.x-mingw.tar.gz\SDL2-2.0.x\x86_64-w64-mingw32\bin 	-> 	gnu-mingw\dll\64
SDL2-devel-2.0.x-mingw.tar.gz\SDL2-2.0.x\i686-w64-mingw32\lib 		-> 	gnu-mingw\lib\32
SDL2-devel-2.0.x-mingw.tar.gz\SDL2-2.0.x\x86_64-w64-mingw32\lib 	-> 	gnu-mingw\lib\64
SDL2-devel-2.0.x-VC.zip\SDL2-2.0.x\lib\x86\*.dll	 		-> 	msvc\dll\32
SDL2-devel-2.0.x-VC.zip\SDL2-2.0.x\lib\x64\*.dll 			-> 	msvc\dll\64
SDL2-devel-2.0.x-VC.zip\SDL2-2.0.x\lib\x86\*.lib	 		-> 	msvc\lib\32
SDL2-devel-2.0.x-VC.zip\SDL2-2.0.x\lib\x64\*.lib	 		-> 	msvc\lib\64

SDL2_image-devel-2.0.x-mingw.tar.gz\SDL2_image-2.0.x\i686-w64-mingw32\bin 		-> 	gnu-mingw\dll\32
SDL2_image-devel-2.0.x-mingw.tar.gz\SDL2_image-2.0.x\x86_64-w64-mingw32\bin 	-> 	gnu-mingw\dll\64
SDL2_image-devel-2.0.x-mingw.tar.gz\SDL2_image-2.0.x\i686-w64-mingw32\lib 		-> 	gnu-mingw\lib\32
SDL2_image-devel-2.0.x-mingw.tar.gz\SDL2_image-2.0.x\x86_64-w64-mingw32\lib 	-> 	gnu-mingw\lib\64
SDL2_image-devel-2.0.x-VC.zip\SDL2_image-2.0.x\lib\x86\*.dll	 		-> 	msvc\dll\32
SDL2_image-devel-2.0.x-VC.zip\SDL2_image-2.0.x\lib\x64\*.dll 			-> 	msvc\dll\64
SDL2_image-devel-2.0.x-VC.zip\SDL2_image-2.0.x\lib\x86\*.lib	 		-> 	msvc\lib\32
SDL2_image-devel-2.0.x-VC.zip\SDL2_image-2.0.x\lib\x64\*.lib	 		-> 	msvc\lib\64

SDL2_ttf-devel-2.0.x-mingw.tar.gz\SDL2_ttf-2.0.x\i686-w64-mingw32\bin 		-> 	gnu-mingw\dll\32
SDL2_ttf-devel-2.0.x-mingw.tar.gz\SDL2_ttf-2.0.x\x86_64-w64-mingw32\bin 	-> 	gnu-mingw\dll\64
SDL2_ttf-devel-2.0.x-mingw.tar.gz\SDL2_ttf-2.0.x\i686-w64-mingw32\lib 		-> 	gnu-mingw\lib\32
SDL2_ttf-devel-2.0.x-mingw.tar.gz\SDL2_ttf-2.0.x\x86_64-w64-mingw32\lib 	-> 	gnu-mingw\lib\64
SDL2_ttf-devel-2.0.x-VC.zip\SDL2_ttf-2.0.x\lib\x86\*.dll	 		-> 	msvc\dll\32
SDL2_ttf-devel-2.0.x-VC.zip\SDL2_ttf-2.0.x\lib\x64\*.dll 			-> 	msvc\dll\64
SDL2_ttf-devel-2.0.x-VC.zip\SDL2_ttf-2.0.x\lib\x86\*.lib	 		-> 	msvc\lib\32
SDL2_ttf-devel-2.0.x-VC.zip\SDL2_ttf-2.0.x\lib\x64\*.lib	 		-> 	msvc\lib\64
```





## Contributing

I aim for this project to be a great place for people just starting with Rust and just starting with Open Source to get involved. I'm pretty green with Rust myself, so any code review, refactorings to idiomatic style, bug fixes and feature PRs are very much appreciated. I have purposely left some features unimplemented before open sourcing with the idea that someone can pick them up as a good first contribution. So please, join in. No developer is too green for this project.

Never made a pull request before? Check out this [5 minute video](https://www.youtube.com/watch?v=rgbCcBNZcdQ) which explains a simple process. Remember to make pull requests against the development branch.

Not sure what to work on? Check out our issues.

## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available, see the [tags on this repository](https://github.com/davejkane/riv/tags).

## Authors

* **[Dave Kane](https://github.com/Davejkane)** - *Initial Implementation*
* **[Alex Gurganus](https://github.com/gurgalex)** - *Implementing core features since 0.1.0*
* **[Nick Hackman](https://github.com/nickhackman)** - *Implementing core features since 0.2.0*

See also the list of [contributors](https://github.com/davejkane/riv/contributors) who participated in this project.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details
