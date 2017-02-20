# Disable the coverage and sanitizer instrumentation for the fuzzer itself.

add_library(LLVMFuzzerNoMainObjects OBJECT
    FuzzerCrossOver.cpp
    FuzzerDriver.cpp
    FuzzerExtFunctionsDlsym.cpp
    FuzzerExtFunctionsDlsymWin.cpp
    FuzzerExtFunctionsWeak.cpp
    FuzzerIO.cpp
    FuzzerIOPosix.cpp
    FuzzerIOWindows.cpp
    FuzzerLoop.cpp
    FuzzerMerge.cpp
    FuzzerMutate.cpp
    FuzzerSHA1.cpp
    FuzzerShmemPosix.cpp
    FuzzerShmemWindows.cpp
    FuzzerTracePC.cpp
    FuzzerTraceState.cpp
    FuzzerUtil.cpp
    FuzzerUtilDarwin.cpp
    FuzzerUtilLinux.cpp
    FuzzerUtilPosix.cpp
    FuzzerUtilWindows.cpp
)

add_library(LLVMFuzzerNoMain STATIC
    $<TARGET_OBJECTS:LLVMFuzzerNoMainObjects>
)

target_link_libraries(LLVMFuzzerNoMain ${LLVM_PTHREAD_LIB})

add_library(LLVMFuzzer STATIC
    FuzzerMain.cpp
    $<TARGET_OBJECTS:LLVMFuzzerNoMainObjects>
)

target_link_libraries(LLVMFuzzer ${LLVM_PTHREAD_LIB})

if(LLVM_INCLUDE_TESTS)
  add_subdirectory(test)
endif()
