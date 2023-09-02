from threading import Thread, Lock, current_thread
from time import sleep
from random import randint

buffer = []
max_buffer_size = 5
buffer_lock = Lock()
terminate_flag = False

def produce():
    global buffer, terminate_flag
    while not terminate_flag:
        item = randint(1, 10)
        buffer_lock.acquire()
        try:
            if len(buffer) < max_buffer_size:
                buffer.append(item)
                print(f"{current_thread().name} Produced: {item}")
        finally:
            buffer_lock.release()
        sleep(1)

def consume():
    global buffer, terminate_flag
    while not terminate_flag:
        buffer_lock.acquire()
        try:
            if len(buffer) > 0:
                item = buffer.pop()
                print(f"{current_thread().name} Consumed: {item}")
        finally:
            buffer_lock.release()
        sleep(1)

producer = Thread(target=produce, name="Producer")
producer1 = Thread(target=produce, name="Producer 1")
consumer = Thread(target=consume, name="Consumer")
consumer1 = Thread(target=consume, name="Consumer 1")

producer.start()
consumer.start()
producer1.start()
consumer1.start()

sleep(3)

terminate_flag = True

producer.join()
consumer.join()
producer1.join()
consumer1.join()

print("Program finished.")
