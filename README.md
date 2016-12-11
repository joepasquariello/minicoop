# minicoop
Minimal cooperative scheduler for Teensy 3.x/LC

Just two external variables (ntasks, curtask) and two external functions (task_create, yield).
minicoop.cpp defines a static array of tasks, with the number of elements as defined by macro
MAX_TASKS in minicoop.h.

    extern uint32_t ntasks;   // number of tasks (1..N)
    extern uint32_t curtask;  // id of current task (0..N-1)
    uint16_t task_create( void(*func)(void *arg), uint32 *stack, size_t stack_size, void *arg );
    void yield( void );
    
The main (system) task is always task 0. It uses the main (system) stack. Calls to
task_create() add tasks 1, 2, etc., each having its own stack as defined by the "stack" and
"stack_size" arguments. Tasks always execute in the order created. Each task must call yield()
to let others run. 
