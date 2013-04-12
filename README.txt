=======
qThread
=======

qThread provides an simplified and safe way to stop long running 
threads.  Typical uses often look like this::

    # Test / Usage of the stoppable thread
    class MyThreadingClass(StoppableThread):
        def __init__(self, a):
            super(MyThreadingClass, self).__init__()
            self.a = a
            self.b = "World"
            self.delay = .5 # seconds
            
        def startup(self):
            # Overload the startup function
            print "My Thread Starting Up..."
            
        def cleanup(self):
            # Overload the cleanup function
            print "My Thread Is Shutting Down..."
            # Close files, ports, etc...
            time.sleep(4)
            print "Cleanup Complete!"
            
        def mainloop(self):
            # Some routine to be called over and over
            # ie: reading ports or sockets
            print self.a + " " + self.b

            # Throttling needs to be done here if the
            # primary function is not blocking
            time.sleep(self.delay)

