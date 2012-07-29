fs     = require 'fs'
{exec} = require 'child_process'

appFiles  = [
    # omit src/ and .coffee to make the below lines a little shorter
    'util'
    'clock'
    'app'
]

task 'build', 'Build single application file from source files', ->
    appContents = new Array remaining = appFiles.length
    for file, index in appFiles then do (file, index) ->
        fs.readFile "src/#{file}.coffee", 'utf8', (err, fileContents) ->
            throw err if err
            appContents[index] = fileContents
            process() if --remaining is 0
    process = ->
        fs.writeFile 'www/lib/app.coffee', appContents.join('\n\n'), 'utf8', (err) ->
            throw err if err
            exec 'coffee --compile www/lib/app.coffee', (err, stdout, stderr) ->
                throw err if err
                console.log stdout + stderr
                fs.unlink 'www/lib/app.coffee', (err) ->
                    throw err if err
                    console.log 'Done.'
