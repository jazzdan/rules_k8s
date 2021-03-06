# Copyright 2017 The Bazel Authors. All rights reserved.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#    http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

load("@io_bazel_rules_k8s//k8s:objects.bzl", "k8s_objects")
load("@k8s_crd//:defaults.bzl", "k8s_crd")
load("@k8s_todo//:defaults.bzl", "k8s_todo")

package(default_visibility = ["//visibility:public"])

licenses(["notice"])  # Apache 2.0

exports_files(["deployment.yaml"])

k8s_crd(
    name = "todo-crd",
    template = ":todo.yaml",
)

k8s_todo(
    name = "example-todo",
    template = ":example.yaml",
)

k8s_objects(
    name = "everything",
    objects = [
        # Create the CRD first.
        ":todo-crd",
        ":example-todo",
    ],
)

k8s_todo(
    name = "joined",
    testonly = 1,
    template = ":joined.yaml",
)

alias(
    name = "staging-apply",
    actual = "//examples/todocontroller/py:controller-deployment.apply",
)
