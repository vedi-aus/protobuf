load("@rules_pkg//pkg:mappings.bzl", "pkg_files", "strip_prefix")
load("@rules_pkg//pkg:tar.bzl", "pkg_tar")
load("//:protobuf_version.bzl", "PROTOBUF_RUST_VERSION")

pkg_tar(
    name = "protobuf_example_crate",
    srcs = [
        ":protobuf_example_files",
        "//:LICENSE",
    ],
    visibility = ["//rust:__subpackages__"],
)

pkg_files(
    name = "protobuf_example_files",
    srcs = [":srcs"],
    strip_prefix = strip_prefix.from_root("rust/release_crates/protobuf_example"),
)

genrule(
    name = "gen_cargo_toml",
    srcs = ["Cargo-template.toml"],
    outs = ["Cargo.toml"],
    cmd = "cat $(SRCS) | sed -e 's/{{VERSION}}/{0}-beta/g' > $(OUTS)".format(PROTOBUF_RUST_VERSION),
)

filegroup(
    name = "srcs",
    srcs = [":gen_cargo_toml"] + glob(["**/*"]),
    visibility = ["//rust:__subpackages__"],
)
