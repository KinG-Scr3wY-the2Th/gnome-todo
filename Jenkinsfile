def base_image = "waltervargas/gnome-todo"

node {
  checkout scm

  stage("Flatpak build"){
    sh "/usr/local/bin/flatpak-builder --user --disable-rofiles-fuse --force-clean --repo=repo dist org.gnome.Todo.Test.json"
  }

  stage("Flatpak build inside docker"){
     def flatpakenv = docker.build "flatpakenv:gnome-todo"
     flatpakenv.inside {
       sh 'flatpak-builder --user --disable-rofiles-fuse --force-clean --repo=repo dist org.gnome.Todo.Test.json'
     }
  }

  stage("Faltpak tests"){
    echo "tests"
    //sh 'flatpak-builder --run dist org.gnome.Todo.Test.json gnome-desktop-testing-runner gnome-todo'
  }
}
