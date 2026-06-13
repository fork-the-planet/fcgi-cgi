project(
  'fcgi-cgi',
  'c',
  default_options: [
    'buildtype=debugoptimized',
    'warning_level=2',
    'c_std=gnu99',
  ],
  version: '0.2.2',
  license: 'BSD-3-Clause',
)

search_includes = include_directories(get_option('search-inc'))
search_libs = get_option('search-lib')

compiler = meson.get_compiler('c')

conf_data = configuration_data()
conf_data.set_quoted('PACKAGE_NAME', meson.project_name())
conf_data.set_quoted('PACKAGE_VERSION', meson.project_version())

warn_c_args = [
  '-fno-strict-aliasing',
  '-Wshadow',
  '-W',
]
if get_option('extra-warnings')
  warn_c_args += [
    '-Wmissing-declarations',
    '-Wdeclaration-after-statement',
    '-Wcast-align',
    '-Wsign-compare',
    # '-Wnested-externs',
    '-Wpointer-arith',
    '-Wmissing-prototypes',
    '-Wno-pointer-sign',
    '-Wformat',
    '-Wformat-security',
    '-D_FORTIFY_SOURCE=2',
    '-fstack-protector',
    '--param=ssp-buffer-size=4',
  ]
endif

dep_glib = dependency('glib-2.0', version: '>=2.16')

# find libev manually
debug('libs:', search_libs)
dep_ev = compiler.find_library(
  'ev',
  has_headers: 'ev.h',
  dirs: search_libs,
  header_include_directories: search_includes,
)
if not compiler.has_function(
  'ev_time',
  prefix: '#include <ev.h>',
  dependencies: dep_ev,
  include_directories: search_includes,
)
  error('Missing ev_time() in libev')
endif

add_project_arguments(
  compiler.get_supported_arguments(warn_c_args),
  language: 'c'
)

subdir('src')

install_man(
  'fcgi-cgi.1',
)
