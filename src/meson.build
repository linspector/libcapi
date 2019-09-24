capi_sources = [
  'capi20.c',
  'capifunc.c',
  'convert.c'
]

capi_mod_std_sources = [
  'capi_mod_std.c'
]

capi_mod_fritzbox_sources = [
  'capi_mod_fritzbox.c'
]

capi_mod_rcapi_sources = [
  'capi_mod_rcapi.c'
]

capi_headers = [
  'capi20.h',
  'capicmd.h',
  'capi_debug.h',
  'capi_mod.h',
  'capiutils.h'
]

cc = meson.get_compiler('c')

capi_dep = []
capi_dep += cc.find_library('dl')
capi_dep += cc.find_library('rt')
capi_dep += dependency('threads')

install_headers(capi_headers)

if host_machine.system() == 'windows'
    capi_plugins_path = join_paths('lib', capi_name)
else
    capi_plugins_path = join_paths(get_option('prefix'), get_option('libdir'), capi_name)
endif

capi_shared = shared_library(capi_name,
                        capi_sources,
                        dependencies : capi_dep,
                        install: true,
                        c_args : '-DLIBDIR="' + capi_plugins_path + '"',
                        version: meson.project_version(),
                        soversion: '3')

capi_shared_dep = declare_dependency(link_with : capi_shared)

capi_mod_std = shared_module('capi_mod_std',
                        capi_mod_std_sources,
                        dependencies : capi_shared_dep,
                        install : true,
                        install_dir : capi_plugins_path)

capi_mod_fritzbox = shared_module('capi_mod_fritzbox',
                        capi_mod_fritzbox_sources,
                        dependencies : capi_shared_dep,
                        install : true,
                        install_dir : capi_plugins_path)

capi_mod_rcapi = shared_module('capi_mod_rcapi',
                        capi_mod_fritzbox_sources,
                        dependencies : capi_shared_dep,
                        install : true,
                        install_dir : capi_plugins_path)

pkg_mod = import('pkgconfig')
pkg_mod.generate(libraries : capi_shared,
                 version : meson.project_version(),
                 name : 'capi20',
                 filebase : 'capi20',
                 description : 'CAPI 2.0 library')