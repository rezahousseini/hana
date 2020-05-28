project('hana', 'cpp', 
  version: '1.6.0',
  license: 'boost',
  default_options : ['warning_level=3', 'cpp_std=c++14']
)

hana_dep = declare_dependency(
  include_directories: include_directories('include')
)

if not meson.is_subproject()
  install_headers('include/boost/hana.hpp', subdir: 'hana')
  
  pkgc = import('pkgconfig')
  pkgc.generate(name: 'hana',
    version: meson.project_version(),
    description: 'Your standard library for metaprogramming'
  )
endif
