set(RUN_OPTIONS < input)
llvm_multisource(hexxagon)
target_include_directories(hexxagon PRIVATE ${CMAKE_CURRENT_SOURCE_DIR})
llvm_test_data(hexxagon input)
