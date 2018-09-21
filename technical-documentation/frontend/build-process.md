# Build process

You can use Gulp comands to build the TPM application. There is difference beetwen building module for development or production.  You can find details on the realisation specific gulp tasks in `gulp-tasks/` directory.

### Development

Use the following command to build an application for development:

```text
gulp devup
```

This comand will run several gulp tasks. It will clean destenation directory,  build source files using polytempl, babel and other plugins, copy necessary assets and bower components. Then it will run node server by executing `express.js` file and start watching changes in application source files.

### Production

You can call default gulp task or use `prodBuild` task to build an application in the production environment. 

```text
gulp 
```

or

```text
gulp prodBuild
```

In this case  Polymer gulp tasks will be used to combine all components into a single file. Also all code will be minifyed. At first it will clean destenation directory, than temporary copy bower components  to `src` directory to allow the Polymer to resolve necessary dependencies, build elements and use Polymer `project.merge(source, dependencies)` task function to combine code.

