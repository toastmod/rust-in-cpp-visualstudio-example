# Calling Rust from C++ in Visual Studio
Here is an example demonstrating a Visual Studio solution that introduces a Rust static library.

# DIY!
If you want to make this youself, you can start by following ["A little Rust with your C"](https://docs.rust-embedded.org/book/interoperability/rust-with-c.html).\
Make sure to grab the [cbindgen.toml template](https://github.com/eqrion/cbindgen/blob/master/template.toml) along the way.

You must use `crate-type = ["staticlib"]` instead of `cdylib` for this, since Visual Studio will statically link for you.

Once you're done, create a new Visual C++ project, mine was the 'Visual C++ > Empty Project' template.\
Set the following settings in your project properties...

- C/C++ > General > Additional Include Directories:
   * `$(ProjectDir)\YOUR_RUST_CRATE_NAME_HERE;%(AdditionalIncludeDirectories)`
   
- Linker > General > Additional Library Directories: 
   * `$(ProjectDir)\YOUR_RUST_CRATE_NAME_HERE\target\debug;%(AdditionalLibraryDirectories)`
   
- Linker > Input > Additional Dependencies: 
   * `YOUR_RUST_CRATE_NAME_HERE.lib;ws2_32.lib;userenv.lib;bcrypt.lib;%(AdditionalDependencies)` 
   * And I couldn't tell ya why the heck `ws2_32.lib;userenv.lib;bcrypt.lib;` are needed to compile :^)
    
Hope this helps for people who are relatively n00bies with Visual Studio :D 


