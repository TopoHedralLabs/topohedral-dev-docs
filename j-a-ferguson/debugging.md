We want 3 levels of state to be available to the user:

- At the finest level the internal state of a thread, so stack-frames, local variables, call-stacks etc, need to be accessible to the user via the VScode GUI as per usual. **This is level1**.
- At the middle level, we need to be able to drive the kernel using python. The exact nature of this is as yet undecided, could run the kernel as an RPC server or wrap it directly using pyo3. At this level we need kernel-level internal inspection:
	- What nodes are currently alive
	- Query the structure of the model
	- Peform modelling operatations
	Crucially, we need to be able to able to attach the debugger to the python-driven middle level when we need fine level debugging to be done in VScode. **This is level 2**
- At the top level we need graphical debugging. We are making ``topohedral-viewer`` accessible as an RPC server. Therefore, when running level 2 debugging we also need to launch the viewer as a separate process which listens to a port. On the ``topohedral-modeller`` side use RPC client code written in python to: 
	- Get information from the modeller either directly (py03 route) or via RPC and send it to the viewer to be rendered.   
	The most advanced level of this will be when topohedral can send requests to the modeller. For example if a develper selects a point on the screen and the viewer can ask the modeller to perform a ray-fire.