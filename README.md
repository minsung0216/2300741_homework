### 2300741 최민성 과제
==========================================================
### 배운내용
(
## 보내는 파일 만들기 
-----------------------------------------------------------------------------------------------------------------------------
pwd를 사용하여 home인지를 확인한다
만약에 위치가 home이면 시작
cd ~/robot_ws/src/my_first_ros_rclpy_pkg/my_first_ros_rclpy_pkg을 입력한 후에 
gedit를 사용해 이름_publisher.py파일을 열고 안에

import rclpy
from rclpy.node import Node
from rclpy.qos import QoSProfile
from std_msgs.msg import String


class 이름Publisher(Node):

    def __init__(self):
        super().__init__('이름_publisher')
        qos_profile = QoSProfile(depth=10)
        self.이름_publisher = self.create_publisher(String, '이름', qos_profile)
        self.timer = self.create_timer(1, self.publish_이름_msg)
        self.count = 0
        
    def publish_이름_msg(self):
        msg = String()
        msg.data = '이름: {0}'.format(self.count)
        self.이름_publisher.publish(msg)
        self.get_logger().info('Published message: {0}'.format(msg.data))
        self.count += 1
        
def main(args=None):
rclpy.init(args=args)
node = 이름Publisher()
    try:
        rclpy.spin(node)
        
    except KeyboardInterrupt:
        node.get_logger().info('Keyboard Interrupt (SIGINT)')
        
    finally:
        node.destroy_node()
        rclpy.shutdown()
        
if __name__ == '__main__':
    main()
    

-----------------------------------------------------------------------------------------------------------------------------
## 만약
이름_publisher.py파일이 없다면 ~/robot_ws/src/my_first_ros_rclpy_pkg/my_first_ros_rclpy_pkg위치에서 
touch 이름_publisher.py
# 그 다음 
~/robot_ws/src/my_first_ros_rclpy_pkg/my_first_ros_rclpy_pkg위치에서 이름_subscriber.py파일을 만들고 이때 
이름은 이름Publisher 에 들어있는 이름과 같아야 된다
gedit 이름_subscriber.py
을 한 후 
-----------------------------------------------------------------------------------------------------------------------------
## 받는 파일 만들기
-----------------------------------------------------------------------------------------------------------------------------
import rclpy
from rclpy.node import Node
from rclpy.qos import QoSProfile
from std_msgs.msg import String


class 이름Subscriber(Node):

    def __init__(self):
        super().__init__('이름_subscriber')
        qos_profile = QoSProfile(depth=10)
        self.이름_subscriber = self.create_subscription(
            String, '이름', self.subscribe_topic_message, qos_profile)
            
    def subscribe_topic_message(self, msg):
        self.get_logger().info('Received message: {0}'.format(msg.data))
        
def main(args=None):
    rclpy.init(args=args)
    node = 이름Subscriber()
    try:
        rclpy.spin(node)
    except KeyboardInterrupt:
        node.get_logger().info('Keyboard Interrupt (SIGINT)')
        
    finally:
        node.destroy_node()
        rclpy.shutdown()
        
if __name__ == '__main__':
    main()
    
-----------------------------------------------------------------------------------------------------------------------------
##실행 해보기
-----------------------------------------------------------------------------------------------------------------------------
을 다 입력했다면 각각
ros2 run my_first_ros_rclpy_pkg 이름_subscriber 과 ros2 run my_first_ros_rclpy_pkg 이름_publisher을 사용하면 된다.
)

# 과제 조건 
"이름" 은 영어로


#제출할 과제 이름 : 최민성 학번 : 2300741
-----------------------------------------------------------------------------------------------------------------------------
 입력 ~$ gedit minsung_publisher.py //보내기 파일

import rclpy
from rclpy.node import Node
from rclpy.qos import QoSProfile
from std_msgs.msg import String


class MinsungPublisher(Node):

    def __init__(self):
        super().__init__('minsung_publisher')
        qos_profile = QoSProfile(depth=10)
        self.minsung_publisher = self.create_publisher(String, 'minsung', qos_profile)
        self.timer = self.create_timer(1, self.publish_minsung_msg)
        self.count = 0
        
    def publish_minsung_msg(self):
        msg = String()
        msg.data = 'Minsung: {0}'.format(self.count)
        self.minsung_publisher.publish(msg)
        self.get_logger().info('Published message: {0}'.format(msg.data))
        self.count += 1
        
def main(args=None):
rclpy.init(args=args)
node = MinsungPublisher()
    try:
        rclpy.spin(node)
        
    except KeyboardInterrupt:
        node.get_logger().info('Keyboard Interrupt (SIGINT)')
        
    finally:
        node.destroy_node()
        rclpy.shutdown()
        
if __name__ == '__main__':
    main()
-----------------------------------------------------------------------------------------------------------------------------
 입력 ~$ gedit minsung_subscriber.py // 받기 파일


import rclpy
from rclpy.node import Node
from rclpy.qos import QoSProfile
from std_msgs.msg import String


class MinsungSubscriber(Node):

    def __init__(self):
        super().__init__('Minsung_subscriber')
        qos_profile = QoSProfile(depth=10)
        self.minsung_subscriber = self.create_subscription(
            String, 'minsung', self.subscribe_topic_message, qos_profile)
            
    def subscribe_topic_message(self, msg):
        self.get_logger().info('Received message: {0}'.format(msg.data))
        
def main(args=None):
    rclpy.init(args=args)
    node = MinsungSubscriber()
    try:
        rclpy.spin(node)
    except KeyboardInterrupt:
        node.get_logger().info('Keyboard Interrupt (SIGINT)')
        
    finally:
        node.destroy_node()
        rclpy.shutdown()
        
if __name__ == '__main__':
    main()
-----------------------------------------------------------------------------------------------------------------------------
