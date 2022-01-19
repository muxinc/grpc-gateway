workspace(name = "com_github_muxinc_grpc_gateway")

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

http_archive(
    name = "io_bazel_rules_go",
    sha256 = "2b1641428dff9018f9e85c0384f03ec6c10660d935b750e3fa1492a281a53b0f",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/rules_go/releases/download/v0.29.0/rules_go-v0.29.0.zip",
        "https://github.com/bazelbuild/rules_go/releases/download/v0.29.0/rules_go-v0.29.0.zip",
    ],
)

load("@io_bazel_rules_go//go:deps.bzl", "go_register_toolchains", "go_rules_dependencies")

http_archive(
    name = "bazel_gazelle",
    sha256 = "de69a09dc70417580aabf20a28619bb3ef60d038470c7cf8442fafcf627c21cb",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/bazel-gazelle/releases/download/v0.24.0/bazel-gazelle-v0.24.0.tar.gz",
        "https://github.com/bazelbuild/bazel-gazelle/releases/download/v0.24.0/bazel-gazelle-v0.24.0.tar.gz",
    ],
)

load("@bazel_gazelle//:deps.bzl", "gazelle_dependencies")
load("//:repositories.bzl", "go_repositories")

go_repositories()

http_archive(
    name = "go_googleapis",
    patch_args = [
        "-E",
        "-p1",
    ],
    patches = [
        # googleapis vendors its own BUILD.bazel files that need to be re-generated
        # to play nicely with Gazelle.
        # 1. Delete vendored BUILD.bazel.
        "@io_bazel_rules_go//third_party:go_googleapis-deletebuild.patch",
        # 2. Add specific Gazelle directives (See: https://github.com/bazelbuild/rules_go/blob/ba7bdfd6b5118d135ae3f7984c94103510bf4167/third_party/go_googleapis-directives.patch)
        "@io_bazel_rules_go//third_party:go_googleapis-directives.patch",
        # 3. Gazelle run.
        "@io_bazel_rules_go//third_party:go_googleapis-gazelle.patch",
    ],
    sha256 = "a85c6a00e9cf0f004992ebea1d10688e3beea9f8e1a5a04ee53f367e72ee85af",
    strip_prefix = "googleapis-409e134ffaacc243052b08e6fb8e2d458014ed37",
    # master, as of 2021-10-06
    urls = [
        "https://storage.googleapis.com/public-bazel-artifacts/bazel/409e134ffaacc243052b08e6fb8e2d458014ed37.zip",
    ],
)

go_rules_dependencies()

go_register_toolchains(version = "1.17.5")

http_archive(
    name = "com_google_protobuf",
    sha256 = "d0f5f605d0d656007ce6c8b5a82df3037e1d8fe8b121ed42e536f569dec16113",
    strip_prefix = "protobuf-3.14.0",
    urls = [
        "https://mirror.bazel.build/github.com/protocolbuffers/protobuf/archive/v3.14.0.tar.gz",
        "https://github.com/protocolbuffers/protobuf/archive/v3.14.0.tar.gz",
    ],
)

load("@com_google_protobuf//:protobuf_deps.bzl", "protobuf_deps")

protobuf_deps()

gazelle_dependencies()
