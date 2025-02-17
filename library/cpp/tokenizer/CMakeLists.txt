
# This file was gererated by the build system used internally in the Yandex monorepo.
# Only simple modifications are allowed (adding source-files to targets, adding simple properties
# like target_include_directories). These modifications will be ported to original
# ya.make files by maintainers. Any complex modifications which can't be ported back to the
# original buildsystem will not be accepted.



add_library(library-cpp-tokenizer)
target_compile_options(library-cpp-tokenizer PRIVATE
  -DCATBOOST_OPENSOURCE=yes
)
target_link_libraries(library-cpp-tokenizer PUBLIC
  contrib-libs-cxxsupp
  yutil
  library-cpp-enumbitset
  library-cpp-langmask
  cpp-token-lite
)
target_sources(library-cpp-tokenizer PRIVATE
  ${CMAKE_SOURCE_DIR}/library/cpp/tokenizer/abbreviations.cpp
  ${CMAKE_SOURCE_DIR}/library/cpp/tokenizer/charclasses.cpp
  ${CMAKE_SOURCE_DIR}/library/cpp/tokenizer/multitokenparser.cpp
  ${CMAKE_SOURCE_DIR}/library/cpp/tokenizer/multitokenutil.cpp
  ${CMAKE_SOURCE_DIR}/library/cpp/tokenizer/nlpparser.cpp
  ${CMAKE_SOURCE_DIR}/library/cpp/tokenizer/sentbreakfilter.cpp
  ${CMAKE_SOURCE_DIR}/library/cpp/tokenizer/split.cpp
  ${CMAKE_SOURCE_DIR}/library/cpp/tokenizer/tokenizer.cpp
  ${CMAKE_SOURCE_DIR}/library/cpp/tokenizer/special_tokens.cpp
)
add_custom_command(
  OUTPUT
  ${CMAKE_BINARY_DIR}/library/cpp/tokenizer/SpecialTokens.rodata
  DEPENDS
  ${CMAKE_BINARY_DIR}/library/cpp/tokenizer/special_tokens.trie
  COMMAND
  ${CMAKE_BINARY_DIR}/tools/archiver/archiver
  -q
  -p
  ${CMAKE_BINARY_DIR}/library/cpp/tokenizer/special_tokens.trie:
  -o
  ${CMAKE_BINARY_DIR}/library/cpp/tokenizer/SpecialTokens.rodata
)
add_custom_command(
  OUTPUT
  ${CMAKE_BINARY_DIR}/library/cpp/tokenizer/special_tokens.trie
  DEPENDS
  ${CMAKE_SOURCE_DIR}/library/cpp/tokenizer/special_tokens.txt
  ${CMAKE_BINARY_DIR}/tools/triecompiler/triecompiler
  WORKING_DIRECTORY
  ${CMAKE_SOURCE_DIR}/library/cpp/tokenizer
  COMMAND
  ${CMAKE_BINARY_DIR}/tools/triecompiler/triecompiler
  ${CMAKE_BINARY_DIR}/library/cpp/tokenizer/special_tokens.trie
  -0
  -i
  ${CMAKE_SOURCE_DIR}/library/cpp/tokenizer/special_tokens.txt
  -w
)
target_ragel_lexers(library-cpp-tokenizer
  PRIVATE
  ${CMAKE_SOURCE_DIR}/library/cpp/tokenizer/nlptok_v2.rl6
  -L
  -G2
)
target_ragel_lexers(library-cpp-tokenizer
  PRIVATE
  ${CMAKE_SOURCE_DIR}/library/cpp/tokenizer/nlptok_v3.rl6
  -L
  -G2
)
target_rodata_sources(library-cpp-tokenizer
  PRIVATE
  ${CMAKE_BINARY_DIR}/library/cpp/tokenizer/SpecialTokens.rodata
)
