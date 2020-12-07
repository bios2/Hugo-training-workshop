# Why this training workshop ? 

I am only 10 hours of a crash course in web development ahead of you. As part of a major research project on setting a biodiversity observation network, I had to develop a prototype of a portal for the project, for biodiversity information and bunch of dashboards on biodiversity trends. Never made a website before. I know how to code in a few langages, and I know that I hate playing with boxes, menus, importing images manually, and most of all, dealing with a crash of the system and having to redo the whole thing because I made a mistake somewhere. Not that a bug when I try to compile is better, but at least it is more tractable. 

Hugo made it very easily because of its fundamental feature (which is the same reason I edit papers with LaTeX): the distinction between the view and the content. Once you have set up the rules defining the visual aspects of the pages, then you can focus on the content and let the software automatically constructing the html code for you. It's fast, accessible, scriptable and could be version-controlled. All qualities for an open and reproducible science.  

Took me a few hours to learn the basics (much harder to get the higher level skills, especially to write your own Go scripts), I took some tricks here and there in different templates and at looking what others do, and that was it I had my website. Realized that it could be a good entry level course to BIOS2 fellows and decided to turn that experience into a training workshop. 

You will find below basic instructions to install and run a template. The following is not a full tutorial, for that I recommend simply to take time looking at the documentation provided on the Hugo page (https://gohugo.io/). I also consulted the online book **Hugo in action** (https://www.manning.com/books/hugo-in-action). There are many other references, all of them with goods and bads. But it's nice to have multiple ones because sometimes the description of a concept may be obscure in one reference but better in the other and it's by comparing and switching between them that you can make progress. 

# Make sure Hugo is installed and check version

First step, you have to make sure that it is properly installed on you computer. Type the following command in terminal to make sure :

```
hugo version
```

You can access to the help menu with the simple command : 

```
hugo help
```


# Be Timothée Poisot for fun

We will use Tim's website, which is a simple but efficient example of what we could achieve with Hugo. The strenght of the website is that it automatically updates with the addition of new content, such as publications, lab members and projects. The only thing you have to do, once the template is properly set up, is to update the content. That way, yo can focus on the material you want to put on, without struggling on how to place the boxes, format the police and all of the complicate stuff that comes with html and css. The content, written in markdown, is human readable and therefore could be easily edited by lab members. Further, since it's all scripted, it's easy to maintain and control versions. 

Take few minutes to look at the final webpage at https://poisotlab.io/

Now you will clone the repository on your own computer so that you could start playing with the content, edit the files, modify list of papers and so on. 

You can either use the clone button on the top of the page or the following command : 

```
git clone https://github.com/bios2/Hugo-training-workshop.git
```

We will take a few minutes to look at the content of the different folders. This structure is common to most of the Hugo templates. You will find multiple folders, it's useful to understand what's located where because the compiler expects this structure when it looks for specific information.  

**archetypes** (not in here, but usually in most templates). These are basic instructions to generate new content with the *hugo new* command. We won't use this feature today, but information about this feature is easy to find. 

**assets** contains the css files where the controls for visual aspect of the pages are specified. That's where you'll search for the different items and how to specify things such as box sizes, font colors and dimensions etc.... Note: assets directory is not created by default.

**content** holds all of the .md files where the main content of the pages is provided. It's divided in several subfolders, corresponding to the different pages from the menu. Each top-level folder in Hugo is considered a content section (which is described usually in the config file). For instance, you have one folder called **Research** where the projects are described. You'll find one .md file per projec tin this folder. Note also that the folders contain systematically a _index.md file where the metadata and the top level information of the page are specified. We'll come back to that later. 

**data** stores specific information that will be consulted by the parser during compilation (configurationfiles). There are also data templates, and at the moment, there is one json file where the papers are listed and two toml files with a list of the students, past and present. json files could be edited with a text editor (not so fun), but there are some tools to do it efficiently. 
 
 **layouts** contains the core files to compile the website. You will find in them instructions, in a strange blend of html and Go langages. No so easy and pleasant to play with, but looking at them tells you a bit about what the compiler does (a good example is for *people*). *list.html* for instance contains a loop that goes through the toml files in order to create the icons, the text and the link to the full markdown page where you have description for each student. You will find layouts for the main pages, as well as for partials (like the header menu). 

 **resources** also contains css instructions for the template. We won't work with this one.

 **static** contains bunch of little things that are called during compilation. You'll find the logo for the lab, the pictures for students, pdf files for applications, images for each research project ...

There is also one very important file in the main folder the **config.toml** file. Inside, you will find a lot of the metadata that will control the structure of the main page. This find can be very simple for some templates, much more complicated for other ones. Note that for some templates, the config file may be in a distinct folder. Not all templates have exactly the same folder structure. 

*toml* is a file format for configuration files, it contains key parameters for the webpage. It consists of key = "value" pairs, [section names], and # comments. Let's open this one to have a closer look. 

## Exercise : Edit the toml file to include your own information. 

You may want to change the section *People* to *Collaborators* and also provide a proper reference to your on github page. You can also add or remove sections, this will affect the menu at the top of the page. For instance, you can add a blog section. 

# Build the static html files

## Build for local development 

Hugo will use all of the material to generate static html files that will be displayed on your browser. The command is really easy to use to run it on your own computer, you simply have to type the following in the main folder : 

```
hugo server
```

And that's it, it compiles and you can simply open it in your browser by clicking on the adress indicated in the terminal. Congratulations for your first Hugo webste ! 

There are useful information in the terminal about the building process. 

## Build for publishing your website

The command *hugo server* is very fast and useful to test your website while you develop it. But once you'll be ready to distribute it, you'll need all of the html files and related material to distribute the website. This is easily done with the even simpler command 

```
hugo
```

You will find in the directory that a new folder named **public** appeared, with all of the material needed to deploy the website. If you click on the *index.html* file, you'll get to the home page of the website. It is interesting to open this file in your text editor, you'll get a sense of the html code that hugo generated automatically for you. You can also take a look at other files. 


# Edit content

Editing content is the easier thing to do. First thing to do, is to modify the content of the introduction paragraph on the main page. You'll find it in the *_index.md* file in the **content** folder. Open it and modify the text. You can after build the main page again to see the update. 

You can also add material, with new md files. We will do so with a new research project (note the following could be done manually): 

```
hugo new research/chapter1.md
```

This will generate a new markdown file, in which you can start adding material. But those files do have a particular structure, so before editing it, we'll take a quick look at another one, *datascience.md*. 

The header section is typical of a markdown file with metadata (in toml or yaml format). You have to specify information to the parser about the title, the image and associated papers. Note that it will work if some of these (e.g. papers) are missing. You can modify the image as well. 

The file here also a particular structure, with the *<!--more-->* marker between two paragraphs. This command indicates that only the first paragraph is displayed on the main page of the **Research** tab, and the full content follows if you click to know more about the project. 

Note that here you can use the basic features of markdown, with headers, bold, italics and so on. You can also include html code directly into the markdown and it should work. That said, it may conflict with higher level instructions in the layout or in the theme and may cause difficulties at building. While it is feasible to add such command, it is not recommended to do so. People rather suggest to use shortcodes (Tomorrow) or to modify the layout of the website.

## Exercise : take 15 minutes to remove Tim's material and replace it by the three chapters of your thesis. 

# Hosting the website on a server

There are many options to host your new website on a server. An easy one, free, and that could be coupled with version control is to run it on github. Full instructions are available here : 

https://gohugo.io/hosting-and-deployment/hosting-on-github/

We will simply follow the instructions copied here for hosting a personal page. Note that you can also develop a page for a project. 

## GitHub User or Organization Pages 

### Step-by-step Instructions

1. Create a <YOUR-PROJECT> (e.g. blog) repository on GitHub. This repository will contain Hugo’s content and other source files.
2. Create a <USERNAME>.github.io GitHub repository. This is the repository that will contain the fully rendered version of your Hugo website.
3. git clone <YOUR-PROJECT-URL> && cd <YOUR-PROJECT>
4. Paste your existing Hugo project into the new local <YOUR-PROJECT> repository. Make sure your website works locally (hugo server or hugo server -t <YOURTHEME>) and open your browser to http://localhost:1313.
5. Once you are happy with the results:
        Press Ctrl+C to kill the server
        Before proceeding run rm -rf public to completely remove the public directory
6. git submodule add -b main https://github.com/<USERNAME>/<USERNAME>.github.io.git public. This creates a git submodule. Now when you run the hugo command to build your site to public, the created public directory will have a different remote origin (i.e. hosted GitHub repository).
7. Make sure the baseURL in your config file is updated with: <USERNAME>.github.io

### Put it Into a Script

You’re almost done. In order to automate next steps create a deploy.sh script. You can also make it executable with chmod +x deploy.sh.

The following are the contents of the deploy.sh script:

```
    #!/bin/sh

    # If a command fails then the deploy stops
    set -e

    printf "\033[0;32mDeploying updates to GitHub...\033[0m\n"

    # Build the project.
    hugo # if using a theme, replace with `hugo -t <YOURTHEME>`

    # Go To Public folder
    cd public

    # Add changes to git.
    git add .

    # Commit changes.
    msg="rebuilding site $(date)"
    if [ -n "$*" ]; then
        msg="$*"
    fi
    git commit -m "$msg"
```

# Push source and build repos.

```
git push origin main
```

You can then run ./deploy.sh "Your optional commit message" to send changes to <USERNAME>.github.io. Note that you likely will want to commit changes to your <YOUR-PROJECT> repository as well.

That’s it! Your personal page should be up and running at https://<USERNAME>.github.io within a couple minutes.