# SPDX-FileCopyrightText: (c) Hanspeter Portner (dev@open-music-kontrollers.ch)
# SPDX-License-Identifier: CC0-1.0

project('varchunk', 'c', default_options : [
	'buildtype=release',
	'warning_level=3',
	'werror=true',
	'b_lto=false',
	'c_std=c11'])

reuse = find_program('reuse', required : false)

add_project_arguments('-D_GNU_SOURCE', language : 'c')

conf_data = configuration_data()
cc = meson.get_compiler('c')

thread_dep = dependency('threads')
deps = [thread_dep]

if host_machine.system() == 'linux'
	rt_dep = cc.find_library('rt')
	deps += rt_dep
endif

test_varchunk = executable('test_varchunk',
	'test_varchunk.c',
	dependencies : deps,
	install : false)

test('Test', test_varchunk,
	args : ['100000'],
	timeout : 360) # seconds

if reuse.found()
  test('REUSE', reuse, args : [
    '--root', meson.source_root(),
    'lint'
  ])
endif
