cc_library(
    name = "vsoc_lib",
    srcs = [
        "common/vsoc/lib/compat.cpp",
        "common/vsoc/lib/e2e_test_region_layout.cpp",
        "common/vsoc/lib/lock_common.cpp",
        "common/vsoc/lib/region_view.cpp",
        "host/vsoc/lib/host_lock.cpp",
        "host/vsoc/lib/region_control.cpp",
        "host/vsoc/lib/region_view.cpp",
    ],
    hdrs = [
        "common/vsoc/lib/circqueue_impl.h",
        "common/vsoc/lib/compat.h",
        "common/vsoc/lib/e2e_test_region_view.h",
        "common/vsoc/lib/graphics_common.h",
        "common/vsoc/lib/lock_guard.h",
        "common/vsoc/lib/region_control.h",
        "common/vsoc/lib/region_view.h",
        "common/vsoc/lib/single_sided_signal.h",
        "common/vsoc/lib/typed_region_view.h",
    ],
    copts = ["-Wno-unused-private-field"],
    visibility = ["//visibility:public"],
    deps = [
        "//common/libs/fs",
        "//common/vsoc/shm",
        "@cuttlefish_kernel//:uapi",
    ],
)

cc_library(
    name = "libvsoc_framebuffer",
    srcs = [
        "common/vsoc/framebuffer/fb_bcast_region.cpp",
        "common/vsoc/lib/fb_bcast_layout.cpp",
    ],
    hdrs = [
        "common/vsoc/framebuffer/fb_bcast_region.h",
    ],
    copts = ["-Wno-unused-private-field"],
    visibility = ["//visibility:public"],
    deps = [
        "//:vsoc_lib",
    ],
)

cc_binary(
    name = "test_framebuffer",
    srcs = ["common/vsoc/framebuffer/test_fb.cpp"],
    deps = ["//:libvsoc_framebuffer"],
)

cc_library(
    name = "libvsoc_gralloc",
    srcs = [
        "common/vsoc/lib/gralloc_layout.cpp",
        "host/vsoc/gralloc/gralloc_buffer_region.cpp",
    ],
    hdrs = [
        "host/vsoc/gralloc/gralloc_buffer_region.h",
    ],
    copts = ["-Wno-unused-private-field"],
    visibility = ["//visibility:public"],
    deps = [
        "//:vsoc_lib",
    ],
)

cc_test(
    name = "circqueue_test",
    srcs = [
        "common/vsoc/lib/circqueue_test.cpp",
    ],
    visibility = ["//visibility:public"],
    deps = [
        ":vsoc_lib",
        "//common/vsoc/shm",
        "@gtest_repo//:gtest_main",
    ],
)

cc_test(
    name = "lock_test",
    srcs = [
        "common/vsoc/lib/lock_test.cpp",
    ],
    visibility = ["//visibility:public"],
    deps = [
        ":vsoc_lib",
        "//common/vsoc/shm",
        "@gtest_repo//:gtest_main",
    ],
)

cc_test(
    name = "vsoc_graphics_test",
    srcs = [
        "common/vsoc/lib/graphics_test.cpp",
    ],
    visibility = ["//visibility:public"],
    deps = [
        "//common/vsoc/shm",
        "@gtest_repo//:gtest_main",
    ],
)

cc_binary(
    name = "host_region_e2e_test",
    srcs = [
        "host/vsoc/lib/host_region_e2e_test.cpp",
    ],
    deps = [
        ":vsoc_lib",
        "//common/vsoc/shm",
        "@glog_repo//:glog",
        "@gtest_repo//:gtest",
    ],
)

cc_binary(
    name = "vnc_server",
    srcs = [
        "host/frontend/vnc_server/VirtualInputDevice.cpp",
        "host/frontend/vnc_server/VirtualInputDevice.h",
        "host/frontend/vnc_server/blackboard.cpp",
        "host/frontend/vnc_server/blackboard.h",
        "host/frontend/vnc_server/frame_buffer_watcher.cpp",
        "host/frontend/vnc_server/frame_buffer_watcher.h",
        "host/frontend/vnc_server/jpeg_compressor.cpp",
        "host/frontend/vnc_server/jpeg_compressor.h",
        "host/frontend/vnc_server/keysyms.h",
        "host/frontend/vnc_server/main.cpp",
        "host/frontend/vnc_server/mocks.h",
        "host/frontend/vnc_server/simulated_hw_composer.cpp",
        "host/frontend/vnc_server/simulated_hw_composer.h",
        "host/frontend/vnc_server/tcp_socket.cpp",
        "host/frontend/vnc_server/tcp_socket.h",
        "host/frontend/vnc_server/virtual_inputs.cpp",
        "host/frontend/vnc_server/virtual_inputs.h",
        "host/frontend/vnc_server/vnc_client_connection.cpp",
        "host/frontend/vnc_server/vnc_client_connection.h",
        "host/frontend/vnc_server/vnc_server.cpp",
        "host/frontend/vnc_server/vnc_server.h",
        "host/frontend/vnc_server/vnc_utils.h",
    ],
    copts = [
        "-Wall",
        "-Werror",
        "-Wno-error-unused",
        "-Wno-error=unused-parameter",
        "-Wno-attributes",
    ],
    linkopts = ["-ljpeg"],
    deps = [
        ":libvsoc_framebuffer",
        ":libvsoc_gralloc",
        ":vsoc_lib",
        "//common/libs/fs",
        "//common/libs/thread_safe_queue",
        "//common/libs/threads",
        "//common/vsoc/shm",
        "@cuttlefish_kernel//:uapi",
        "@glog_repo//:glog",
    ],
)
