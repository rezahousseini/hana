project('hana', 'cpp', 
  license: 'boost',
  default_options : ['warning_level=0', 'cpp_std=c++14']
)

hana_dep = declare_dependency(
  include_directories: include_directories('include')
)

if not meson.is_subproject()
  install_headers('include/boost/hana.hpp')
  install_subdir('include/boost/hana', 
    install_dir : 'boost/hana', 
    strip_directory : true,
  )
  
  pkgc = import('pkgconfig')
  pkgc.generate(name: 'hana',
    url : 'http://boostorg.github.io/hana/',
    description: 'Your standard library for metaprogramming',
  )
endif

cxx = meson.get_compiler('cpp')

if cxx.get_id() == 'msvc'
  cpp_args = ['-EHsc', '-bigobj', '-Zc:ternary']
else
  cpp_args = [
    '-fdiagnostics-color',
    '-ftemplate-backtrace-limit=0',
    '-pedantic',
    '-Wall',
    '-Werror',
    '-Wextra',
    '-Wno-self-assign-overloaded',
    '-Wno-unused-local-typedefs',
    '-Wwrite-strings',
  ]
endif

if get_option('BOOST_HANA_ENABLE_EXCEPTIONS').disabled()
  cpp_args += ['-fno-exceptions']
endif

if get_option('BOOST_HANA_ENABLE_CONCEPT_CHECKS').disabled()
  cpp_args += ['-DBOOST_HANA_CONFIG_DISABLE_CONCEPT_CHECKS']
endif

if get_option('BOOST_HANA_ENABLE_DEBUG_MODE').enabled()
  cpp_args += ['-DBOOST_HANA_CONFIG_ENABLE_DEBUG_MODE']
endif

if get_option('BOOST_HANA_ENABLE_STRING_UDL').enabled()
  if cxx.get_id() != 'msvc'
    cpp_args += ['-DBOOST_HANA_CONFIG_ENABLE_STRING_UDL']

    if build_machine.system() != 'gnu'
      cpp_args += ['-Wno-gnu-string-literal-operator-template']
    endif
  endif
endif

boost_dep = dependency('boost', version : '>=1.64', required : false)

valgrind_prog = find_program('valgrind', required : false)
