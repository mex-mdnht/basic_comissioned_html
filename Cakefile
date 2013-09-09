{exec} = require 'child_process'
Rehab = require 'rehab'

#パッケージするcoffeescriptソースのルートフォルダ
source_dir = ''

#書き出すファイルパス
build_file = ''

#最優先読み込みするファイル
before_list = [
]

#最後に読み込むファイル
after_list = [
	
]

#Option
option "-t", "--targetdirectory [folder]", "specify build target"

build = (options)->
	
	console.log "Building project from #{ options.targetdirectory }"
	if(options.targetdirectory?)
		source_dir = options.targetdirectory
		targetdirectory = options.targetdirectory#.split("\\src\\")[1]
		path = targetdirectory.replace("_coffee", "js")
		directories= targetdirectory.split("\\")
		
		
		build_file = "#{ path }.js"
		console.log("build to",build_file)
		

	files = new Rehab().process source_dir
	mix_list = before_list.concat(after_list)
	filter_list = []
	for i in [0...files.length]
		unless files[i] in mix_list
			filter_list.push(files[i])

	to_single_file = "--join #{build_file}"
	from_files = "--compile #{before_list.join ' '} #{filter_list.join ' '} #{after_list.join ' '}"

	exec "coffee #{to_single_file} #{from_files}", (err, stdout, stderr) -> 
		throw err if err

#Mac,Linux用
task 'build', 'Build coffee2js using Rehab', (options)->
	build(options)

#Win用
task 'build_win', 'Build coffee2js using Rehab', (options)->
	for i in [0...before_list.length]
		before_list[i] = before_list[i].replace('/', '\\')
	for i in [0...after_list.length]
		after_list[i] = after_list[i].replace('/', '\\')
	build(options)

