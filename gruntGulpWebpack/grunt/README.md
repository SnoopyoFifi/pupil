# Grunt

- `package.json`

```json

  {
    "name": "static",
    "version": "1.0.0",
    "description": "",
    "main": "Gruntfile.js",
    "dependencies": {},
    "devDependencies": {
      "grunt": "^1.0.1",
      "grunt-contrib-clean": "^1.0.0",
      "grunt-contrib-compass": "^1.1.1",
      "grunt-contrib-concat": "^1.0.1",
      "grunt-contrib-copy": "^1.0.0",
      "grunt-contrib-jshint": "^1.0.0",
      "grunt-contrib-requirejs": "^1.0.0",
      "grunt-contrib-uglify": "^2.0.0",
      "grunt-contrib-watch": "^1.0.0",
      "grunt-tmod": "^0.2.10"
    },
    "scripts": {
      "test": "echo \"Error: no test specified\" && exit 1"
    },
    "keywords": [],
    "author": "snoopy",
    "license": "ISC"
  }

```

- `Gruntfile.js`

```js

  module.exports = function(grunt) {
    // 项目配置
    grunt.initConfig({
      pkg: grunt.file.readJSON('package.json'),

      clean: {
        build: {
          src: ["tmp/*.*"]
        }
      },
      copy: {
        others: {
          files: [{
            expand: true,
            cwd: 'images',
            src: '**/*.*',
            dest: 'tmp/images'
          }, {
            expand: true,
            cwd: 'fonts',
            src: '**/*.*',
            dest: 'tmp/fonts'
          }, {
            expand: true,
            cwd: 'flash',
            src: '**/*.*',
            dest: 'tmp/flash'
          }]
        }
      },
      jshint: {
        files: ['js/**/*.js',
          '!js/**/template.js',
          '!js/lib/**/*.js'
        ],
        options: {
          curly: true,
          eqeqeq: true,
          immed: true,
          latedef: true,
          newcap: true,
          noarg: true,
          sub: true,
          undef: true,
          unused: false,
          boss: true,
          eqnull: true,
          browser: true,
          node: true,
          globals: {
            jQuery: true
          }
        }
      },
      tmod: {
        template: {
          src: 'tpls/**/*.html',
          dest: 'js/common/template.js',
          options: {
            base: 'tpls'
          }
        }
      },
      requirejs: {
        minjs: {
          options: {
            baseUrl: 'js',
            dir: 'tmp/js',
            keepBuildDir: true,
            mainConfigFile: 'config.js',
            modules: [{
              name: 'common/base',
              exclude: [
                'jquery',
                'bootstrap',
                'common/template'
              ]
            }]
          }
        }
      },
      compass: {
        compile: {
          options: {
            sassDir: 'sass',
            cssDir: 'css',
            imagesDir: 'images',
            //httpPath: "../..",
            relativeAssets: true,
            environment: 'development' //'development' //production
          }
        },
        publish: {
          options: {
            sassDir: 'sass',
            cssDir: 'tmp/css',
            imagesDir: 'images',
            httpPath: "/static/",
            httpImagesPath: '/static/images',
            httpGeneratedImagesPath: '/static/images',
            //relativeAssets: true,
            //outputStyle: 'compressed',
            environment: 'production' //'development' //production
          }
        }
      },
      watch: {
        sass: {
          files: ['sass/**/*.scss'],
          tasks: ['compass'],
          options: {
            spawn: true
          }
        },
        template: {
          files: ['tpls/**/*.html'],
          tasks: ['tmod'],
          options: {
            spawn: true
          }
        }
      }
    });

    //加载插件
    grunt.loadNpmTasks('grunt-tmod'); //模板引擎
    grunt.loadNpmTasks('grunt-contrib-concat'); //合并
    grunt.loadNpmTasks('grunt-contrib-jshint'); //语法检测
    grunt.loadNpmTasks('grunt-contrib-uglify'); //压缩
    grunt.loadNpmTasks('grunt-contrib-watch'); //代码变化监控
    grunt.loadNpmTasks('grunt-contrib-requirejs'); //requirejs打包压缩
    grunt.loadNpmTasks('grunt-contrib-compass'); //压缩compass
    grunt.loadNpmTasks('grunt-contrib-copy'); // 复制
    grunt.loadNpmTasks('grunt-contrib-clean'); // 清除

    //任务列表
    grunt.registerTask('test', ['clean']);

    grunt.registerTask('default', ['clean', 'compass:compile', 'tmod']);
    grunt.registerTask('publish', ['clean', 'compass:publish', 'tmod', 'requirejs:minjs', 'copy:others']);
  }


```
