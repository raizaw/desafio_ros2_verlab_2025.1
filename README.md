# README - Simulação Scout Mini no Gazebo com ROS 2 Humble

## Requisitos

- **ROS 2 Humble**
- **Gazebo Fortress**
- **Ubuntu 22.04** (recomendado)

## Instalação do ROS 2 Humble

Para instalar o ROS 2 Humble, siga as instruções oficiais:
[Guia de Instalação](https://docs.ros.org/en/humble/Installation/Ubuntu-Install-Debs.html)

### Passos resumidos:

1. Configurar o locale:
   ```bash
   sudo apt update && sudo apt install locales
   sudo locale-gen en_US en_US.UTF-8
   sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
   export LANG=en_US.UTF-8
   ```
2. Adicionar os repositórios do ROS 2:
   ```bash
   sudo apt install software-properties-common
   sudo add-apt-repository universe
   sudo apt update && sudo apt install curl -y
   sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg
   echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
   sudo apt update
   sudo apt upgrade
   ```
3. Instalar o ROS 2 Humble:
   - **Versão completa (recomendada):**
     ```bash
     sudo apt install ros-humble-desktop
     ```
   - **Versão básica (sem GUI):**
     ```bash
     sudo apt install ros-humble-ros-base
     ```
   - **Ferramentas de desenvolvimento:**
     ```bash
     sudo apt install ros-dev-tools
     ```

### Configuração do ambiente

Para configurar o ambiente, faça o sourcing do seguinte script:

```bash
# Substitua ".bash" pelo seu shell se não estiver usando bash
# Valores possíveis: setup.bash, setup.sh, setup.zsh
source /opt/ros/humble/setup.bash
```

## Instalação do Gazebo Fortress

Para instalar o Gazebo Fortress, siga as instruções:
[Guia de Instalação](https://gazebosim.org/docs/fortress/install_ubuntu/)

### Passos resumidos:

```bash
sudo apt-get update
sudo apt-get install lsb-release gnupg
sudo curl https://packages.osrfoundation.org/gazebo.gpg --output /usr/share/keyrings/pkgs-osrf-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/pkgs-osrf-archive-keyring.gpg] http://packages.osrfoundation.org/gazebo/ubuntu-stable $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/gazebo-stable.list > /dev/null
sudo apt-get update
sudo apt-get install ignition-fortress
```

## Pacotes Adicionais Necessários

Para construir e rodar a simulação corretamente, instale os seguintes pacotes:

```bash
sudo apt install python3-colcon-core python3-colcon-common-extensions
sudo apt install ros-humble-ros-gz-bridge
sudo apt install ros-humble-ros-gz-image
sudo apt install ros-humble-ros-gz-sim
sudo apt install ros-humble-xacro
sudo apt install ros-humble-nav2-common
sudo apt install ros-humble-ament-cmak
```

## Executando a Simulação

1. Clone o repositório:
   ```bash
   git clone https://github.com/raizaw/desafio_ros2_verlab_2025.1.git
   cd desafio_ros2_verlab_2025.1
   ```
2. Construa o pacote:
   ```bash
   colcon build
   ```
3. Faça o sourcing dos pacotes construídos:
   ```bash
   source install/setup.bash
   ```
4. Inicie o ambiente de simulação:
   ```bash
   ros2 launch scout_gazebo_sim scout_mini_empty_world.launch.py
   ```
5. Em outro terminal, controle o robô com o teclado:
   ```bash
   ros2 run teleop_twist_keyboard teleop_twist_keyboard
   ```


