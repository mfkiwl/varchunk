project('varchunk', 'c', default_options : [
	'buildtype=release',
	'warning_level=3',
	'werror=true',
	'b_lto=true',
	'c_std=c11'])

version = run_command('cat', 'VERSION').stdout().strip()

add_project_arguments('-D_GNU_SOURCE', language : 'c')

conf_data = configuration_data()
cc = meson.get_compiler('c')

rt_dep = cc.find_library('rt')
thread_dep = dependency('threads')

test_varchunk = executable('test_varchunk',
	'test_varchunk.c',
	dependencies : [rt_dep, thread_dep],
	install : false)

test('Test', test_varchunk)
