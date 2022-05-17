## Compress images using a pre-commit hook.

## Introduction

Hello everyone, I'm [Apoorv](https://twitter.com/apoorv_taneja) and in this small blog, I'll be explaining how to create a pre-commit hook to compress images.

As we all know there are multiple ways to compress images before pushing the code to production. One of them is to set up a pre-commit hook. 
At work, developers in my team had to manually compress the image before pushing it to production, so I came up with a solution to compress images before committing, so it becomes easy for them and saves time as well. 

So without any delay, let's get our hands dirty

## Steps


1. Install husky and set up pre-commit hook file. For setting up, you can refer to [husky docs](https://typicode.github.io/husky/#/).

2. Now we'll write the bash script for compressing images.

   In this blog, I'm only covering `SVG` formats, you can definitely add a compressor for different types 
   of image formats (`png, jpeg, jpg, etc`).

3. In the pre-commit file, we'll check if `svgo` is installed for compressing images.  

     ```bash
     #!/bin/sh
     . "$(dirname "$0")/_/husky.sh"

     command -v ./node_modules/.bin/svgo >/dev/null 2>&1 || { 
         echo "\033[1mPlease install svgo to reduce images size before commit\033[0m" 
         echo "Install svgo as a devDependency using npm install -D svgo" 
         exit 1;
     }
     ```
4. Now we need to find all the SVG files that are added, renamed, changed or modified in the codebase. 
  we can get that using the command.

     `git diff --diff-filter=ACMRT --cached --name-only | grep ".svg\$"`

 Continuing with our script, we'll find all those files and loop over them. 

     ```
     for file in `git diff --diff-filter=ACMRT --cached --name-only | grep ".svg\$"`
     do 
         ...
         ...
         ...
     done
     ```

5. We will provide an option to the developer if they want to compress a particular `svg` or not. 

     ```
       for file in `git diff --diff-filter=ACMRT --cached --name-only | grep ".svg\$"`
       do 
         exec < /dev/tty 
         read -p "Do you want to compress $file? [yN]: " yn 
         case $yn in 
             ...
             ...
         esac 
       done
     ```

     This is a switch case, where we ask the user to input either `Y` or `y` for compressing the image.
![Screenshot 2022-05-18 at 12.23.40 AM.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1652813954768/sjC78n-vW.png align="left")

6. Now we have to write the code for compressing the SVG file if the user inputs `y`.

```
    case $yn in 
        [Yy]* ) 
            echo "Compressing $file" 
            ./node_modules/.bin/svgo $file -o ${file%.svg}.new 
            mv -f ${file%.svg}.new $file
            git add $file;;
        * ) echo "Skipping $file" && continue;; 
    esac 
```

![Screenshot 2022-05-18 at 12.23.52 AM.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1652813956791/W9yVR2dX7.png align="left")


In the first line, we are compressing the image and storing it with the name `${file}.svg.new`
Then we'll force move the file to its original extension `${file}`. And then add it to the commit.

If the user inputs anything other than `Y` or `y`, we'll skip the compression for that particular file and continue with other files.


That's all, you have built a simple pre-commit hook to compress the images before committing them.

Checkout the code here - [Code link](https://gist.github.com/plxity/db387ae653d8e4c9e7b77a65a67982d5)

## Enhancements

1. Adding support for multiple image formats.
2. Publish it as a package.

-----------------------------------------------------------------------------------------------------------
Thanks for reading this mini blog. 
Connect with me on - [Twitter](https://twitter.com/apoorv_taneja), [GitHub](https://github.com/plxity)


  
