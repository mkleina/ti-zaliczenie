# Przykładowy plik markdown
## Jak powstał ten plik?
Najpierw został zainstalowany moduł gulp-markdown:

    npm install --save-dev gulp-markdown

Po pomyślnej instalacji w pliku gulpfile.babel.js zaimportowałem moduł:

    import markdown from 'gulp-markdown'

Dodałem nowy task markdowns do serii "build":

    gulp.task('build',
      gulp.series(clean, gulp.parallel(pages, markdowns, sass, javascript, images, copy), styleGuide));

Następnie w tym samym pliku zaimplementowałem task markdowns(), który konwertuje wszystkie pliki Markdown do formatu HTML, włączając je jednocześnie do layoutu za pomocą panini:

    function markdowns() {
      return gulp.src('src/pages/**/*.md')
        .pipe(markdown())
        .pipe(panini({
          layouts: 'src/layouts/'
        }))
        .pipe(gulp.dest(PATHS.dist));
    }

> W ten sposób strony mogą być umieszczane w folderze pages zarówno w formacie HTML jak i MD