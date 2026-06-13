configure_file(output: 'config.h', configuration: conf_data)

bin_worker = executable(
  'fcgi-cgi',
  'fcgi-cgi.c',
  'fastcgi.c',
  install: true,
  dependencies: [dep_glib, dep_ev],
  include_directories: search_includes,
)
