import pty
import os

class DeviceEmulator(object):
    def __init__(self, name):
        self.master, slave = pty.openpty()
        self.port = os.ttyname(slave)
        self.name = name

    def write(self, data):
        os.write(self.master, data)

    def read(self, buffer=100):
        data = ''
        while not data: # block
            data = os.read(self.master, buffer)
        self.write(self.parse_command(data))

    def parse_command(self, data):
        if data.startswith('RID'):
            return self.name
        else:
            return "ERR\r\n"


    def getPort(self):
        return self.port
