def base_image = "waltervargas/gnome-todo"

node {
  checkout scm

  stage("Build"){
    sh """
       export FLATPAK_USER_DIR=$HOME/.local/share/flatpak
       flatpak-builder --force-clean --repo=repo dist org.gnome.Todo.Test.json
"""
  }

  stage("Test"){
    sh """
       PATH=$PATH:/usr/local/bin
       flatpak-builder --verbose --run dist org.gnome.Todo.Test.json gnome-desktop-testing-runner gnome-todo > test-suite.log
"""
    step([$class: "TapPublisher", testResults: "test-suite.log"])
  }
}
