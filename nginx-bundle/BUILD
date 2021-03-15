load("@io_bazel_rules_docker//container:container.bzl", "container_bundle", "container_image")
load("@io_bazel_rules_docker//docker/package_managers:download_pkgs.bzl", "download_pkgs")
load("@io_bazel_rules_docker//docker/package_managers:install_pkgs.bzl", "install_pkgs")

download_pkgs(
  name = "nginx_pkgs",
  image_tar = "@ubuntu1804//image",
  packages = ["nginx"],
)

install_pkgs(
  name = "nginx_image",
  image_tar = "@ubuntu1804//image",
  installables_tar = ":nginx_pkgs.tar",
  installation_cleanup_commands = "rm -rf /var/lib/apt/lists/*",
  output_image_name = "nginx_image",
)

container_image(
    name = "release_image",
    base = ":nginx_image.tar",
    stamp = True,
)

container_bundle(
  name = "bundle",
  images = {
    "nginx_bazel:latest": ":release_image",
  },
)
