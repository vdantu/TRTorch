config_setting(
    name = "use_pre_cxx11_abi",
    values = {
        "define": "abi=pre_cxx11_abi",
    }
)

filegroup(
    name = "jit_models",
    srcs = glob(["**/*.jit.pt"])
)

test_suite(
    name = "test_modules",
    tests = [
        ":test_modules_as_engines",
        ":test_compiled_modules",
        ":test_multiple_registered_engines"
    ]
)

cc_test(
    name = "test_multiple_registered_engines",
    srcs = ["test_multiple_registered_engines.cpp"],
    deps = [
        ":module_test",
    ],
    data = [
        ":jit_models"
    ]
)

cc_test(
    name = "test_modules_as_engines",
    srcs = ["test_modules_as_engines.cpp"],
    deps = [
        ":module_test"
    ],
    data = [
        ":jit_models"
    ]
)

cc_test(
    name = "test_compiled_modules",
    srcs = ["test_compiled_modules.cpp"],
    deps = [
        ":module_test"
    ],
    data = [
        ":jit_models"
    ]
)

cc_library(
    name = "module_test",
    hdrs = ["module_test.h"],
    deps = [
        "//cpp/api:trtorch",
        "//tests/util",
        "@googletest//:gtest_main",
    ] + select({
        ":use_pre_cxx11_abi":  ["@libtorch_pre_cxx11_abi//:libtorch"],
        "//conditions:default":  ["@libtorch//:libtorch"],
    }),
)
