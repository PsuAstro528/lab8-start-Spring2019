# Astro 528 Lab 8

Before starting this lab, make sure you've successfully gotten setup to use git, Jupyter, Julia.
The first lab contained detailed instructions for using the Jupyter notebook server.  

For this lab, you'll develop a small Julia package and reflect on your progress twoards your goals for the semester.  I suggest that you add you respond to the questions in this README.md file (in your private repository).  
Remember, that you need follow the link provided via a course announcement to create your own private copy of this lab's repository on GitHub.com.   See the
[help on the course website](https://psuastro528.github.io/lessons/how-to-use-aci/) for instructions on cloning, commiting, pushing and submiting your work.  

## Exercise 1:  Creating a Module & Package
#### Goals:  
- Create a Julia package
- Organize your code using a module

Instructions for [creating a Julia Package](https://julialang.github.io/Pkg.jl/v1/creating-packages/)

1.  Use [`Pkg.generate("ExamplePkg")`] to create a new directory with the bare-bone minimal files for your package (ExamplePkg/Project.toml and ExamplePkg/src/ExamplePkg.jl).  Feel fre to pick your own package name.
If you might want to officially register your package, then review the [recommended conventions for package naming](https://julialang.github.io/Pkg.jl/v1/creating-packages/#Package-naming-guidelines-1) before picking your name.
```julia
julia -e 'using Pkg; Pkg.generate("ExamplePkg")' 
```
2. Change into directory `cd ExamplePkg`, copy any other files you'd like to be in your package into the directory from the beginning and use git to add and commit them to your repository.  Those might include:
   - a [LICENSE](https://github.com/PsuAstro528/lab5-start/blob/master/LICENSE) so others know how you'd like your code to be used
   - [.gitignore](https://github.com/PsuAstro528/lab5-start/blob/master/.gitignore) if there are some files that you don't want added to your git repository
```sh
cp PATH/LICENSE .
cp PATH/.gitignore .
```

3.  Make your directory into a git repository.  Add and commit the current files.  
```sh
git add .
git commit -m "init commit"
```

4. Go to [GitHub](https://github.com) and click the green "New" button to create a new repository.  
   - Enter a repostiory name that matches your repository name, but ends in ".jl",  e.g., "ExamplePkg.jl".  
   - Add a brief description (optional)
   - Choose whether you'd like your repository to be public or private.  Do _not_ check "Initialize this repository with a README".  Select None for "Add .gitignore" and "Add a license".  
   - Click "Create Repository"
   - Copy the code under "or push an existig repository from the command line"
   - Run that code in the directory you create in step 2.
```sh
git remote add origin git@github.com:eford/ExamplePkg.jl.git
git push -u origin master
```
   - Reload the webpage to make sure your files were successfully pushed to GitHub.

5.  Add some trivial code to your package.  For example, in my [`src/ExamplePkg.jl`](https://github.com/eford/ExamplePkg.jl/blob/master/src/ExamplePkg.jl) I have
```julia
module ExamplePkg

using Distributions

export pdf_normal

function pdf_normal(x::Number, mu::Number, sigma::Number)
  dist = Normal(mu,sigma)
  pdf(dist,x)
end

end # module
```

6.  Add any project dependancies to your project's Project.toml and Manifest.toml files.  Note that you don't edit those files manually.  They are updated for you by using `Pkg.add("PackageName")`.  In the example above, I used the [Distributions.jl](https://github.com/JuliaStats/Distributions.jl) package, so I'd do
```julia
using Pkg
Pkg.activate(".")
Pkg.add("Distributions")
```

7.  Add some tests to your package.
   - Create a test/runtests.jl file
```sh
mkdir -p test && touch test/runtests.jl 
```
   - Edit test/runtests.jl to include tests like we've been practicing.  For a reminder, you can see my example [test/runtests.jl]().  Since youru tests will make use of the Test package, add that to the list of dependancies.
```sh
julia -e 'using Pkg; Pkg.activate("."); Pkg.add("Test")'
```
   - Try running your tests using the package manger
```julia
julia -e 'using Pkg; Pkg.actviate("."); Pkg.test("ExamplePkg")'
```
   - Optionally, add a [.travis.yml](https://github.com/PsuAstro528/lab5-start/blob/master/.travis.yml) file, if you've like to enable Continuous Integration testing

   - Add & commit your changes and push to GitHub.

8.  (Optinal) Add/commmit/push any other files that will help potential users make use of your package more easily.  This isn't important for the lab exercise, but could be important if you wanted to shared your project.  For example,

   - README.md if you'd like to provide users an overview of how to install, use, cite, the code in your project.
   - [docker-compose.yml](https://github.com/PsuAstro528/lab5-start/blob/master/docker-compose.yml) if you want to make your package avaliable via Docker
   - [REQUIRE](https://github.com/PsuAstro528/lab5-start/blob/master/REQUIRE) if you want to make your repository avaliable via [mybinder.org](https://mybinder.org/)
   - [environment.yml](https://github.com/PsuAstro528/lab5-start/blob/master/environment.yml) if your repository calls python and you want to have your repository avaliable via [mybinder.org](https://mybinder.org/).
```julia
```
 
9.  Test that others can add your (unregistered package).
   - Exit Julia and change into a new directory.
   - Try installing your package from github
```sh
julia -e 'using Pkg; Pkg.add(PackageSpec(url="https://github.com/eford/ExamplePkg.jl"))'

```

10. Add a link to the github Repo your new package below.

INSERT URL

11. Add other nice features to your project.  For example, if you want code to be run whenever your package in installed (e.g., downloading large datafiles), you can put that code in [`deps/build.jl`](https://julialang.github.io/Pkg.jl/v1/creating-packages/#Adding-a-build-step-to-the-package.-1).  


12. (Optional) Register your package.  If you're interested in sharing your project code with others, then I'd suggest turning it into a Julia package.  Even better, you could _register_ your package, so that others can easily install it.  Unfortunately, the [process for registering packages is scheduled to change on Monday](https://discourse.julialang.org/t/switching-package-registration-systems-on-monday/22677?u=bicycle1885).  So I'd suggest waiting a week or two and then registering your package with the [Registrator.jl](https://github.com/JuliaComputing/Registrator.jl), so that any kinks get ironed out before registering your package.  

## Exercise 2:  Reflect on Goals for Semester
#### Goals:  
- Appreciate how much you've learned and what good habits you've developed during the semester.
- Identify goals which you hope to continue working beyond this semester.
- Develop a plan for building skills that you wish to develop.

Review your personal goals for the class (see Lab 1, Ex 3).  
Which goals were you successfull at making progress towards?

INSERT RESPONCE


Are there some goals that you would change or remove, based on what you've learned during the course?

INSERT RESPONCE

Are there some goals that you would like to continue working towards beyond this semester?

INSERT RESPONCE

What can you do, so as to increase the chances that you'll develop those skills/habits while a graduate student?

INSERT RESPONCE

Remember to commit often, push your repository to GitHub and create a pull request as if you wanted to merge your work (presumably in your master branch) into the original branch (which contains the starter code). 

