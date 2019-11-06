project('cpr', 'cpp', 
    version : '1.3.0', 
    license : 'MIT', 
    default_options : ['cpp_std=c++14']
)

static_build_option = get_option('static_build')

curl_dep = dependency('libcurl', static: static_build_option)

thread_dep = dependency('threads', static: static_build_option)



includes = include_directories('include')
subdir('cpr')

linker_flags = []

if static_build_option
	
    cpr_lib = static_library(
        'cpr', 
        include_directories: includes,
        sources: cpr_src,
        dependencies: [curl_dep, thread_dep],
        link_args: ['-static'])
else
    ssl_dep = dependency('libssl')
    crypto_dep = dependency('libcrypto')
    zlib_dep = dependency('zlib')
    cares_dep = dependency('libcares')
    idn2_dep = dependency('libidn2')

    cpr_lib = shared_library(
        'cpr', 
        include_directories: includes,
        sources: cpr_src,
        dependencies: [curl_dep, thread_dep, ssl_dep, crypto_dep, zlib_dep, cares_dep, idn2_dep])
endif


cpr_dep = declare_dependency(
    include_directories: includes, 
    link_with: cpr_lib)