project(
    'nanopb',
    'c',
    license: 'zlib',
    version: '1.0.0'
)

c_args = []
link_with = []
include_directories = include_directories('.')

sources = files(
    'pb_common.c',
    'pb_encode.c',
    'pb_decode.c'
)

build_common = false

if get_option('encoder').enabled()
    sources += files('pb_encode.c')
    build_common = true
endif

if get_option('decoder').enabled()
    sources += files('pb_decode.c')
    build_common = true
endif

if build_common
    sources += files('pb_common.c')
endif

if get_option('default_library') == 'static'
    nanopb_lib = static_library(
        'nanopb',
        sources,
        c_args: c_args,
        include_directories: include_directories)
else
    nanopb_lib = shared_library(
        'nanopb',
        sources,
        c_args: c_args,
        include_directories: include_directories)
endif

link_with += nanopb_lib

nanopb_dep = declare_dependency(
    include_directories: include_directories,
    link_with: link_with,
)

meson.override_dependency('nanopb', nanopb_dep)
