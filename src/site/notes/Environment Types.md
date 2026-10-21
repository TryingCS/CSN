---
{"dg-publish":true,"permalink":"/environment-types/","created":"2026-10-17T17:55:47.489+01:00","updated":"2026-10-17T18:00:52.914+01:00","dg-note-properties":{}}
---

#krr 
###  Properties of the Environment

The environment dictates how complex the agent's job will be. The slides outline five key ways to classify environments:

1. **Accessible vs. Inaccessible:**
    
    - **Accessible:** The agent can obtain complete, exact, and up-to-date information about the environment's state. (Easy for the agent).
        
    - **Inaccessible:** The agent cannot get complete information (the environment is too complex). (Requires the agent to remember and guess).
        
2. **Deterministic vs. Non-Deterministic:**
    
    - **Deterministic:** Every action guarantees a single, predictable effect. There is no uncertainty about the resulting state.
        
    - **Non-Deterministic:** Actions can have multiple possible outcomes (uncertainty).
        
3. **Static vs. Dynamic:**
    
    - **Static:** The environment does not change while the agent is deliberating (thinking).
        
    - **Dynamic:** The environment can change without the agent's action (between two perceptions).
        
4. **Discrete vs. Continuous:**
    
    - **Discrete:** There is a finite number of possible actions or states (like a chessboard).
        
    - **Continuous:** The states or actions flow infinitely (like driving a car).
        
5. **Single-agent vs. Multi-agent:**
    
    - **Single-agent:** Only one agent is operating in the environment.
        
    - **Multi-agent:** Multiple agents are interacting in the same environment.
        

_Examples from the slides:_

- **Medical Diagnosis System:** Environment = Patient, Hospital, Personnel. Sensors = Keyboard (symptoms). Actuators = Screen (tests, treatments). Performance = Patient's health.
    
- **Taxi Driver:** Environment = Roads, other cars, pedestrians. Sensors = Cameras, speedometer. Actuators = Steering wheel, brakes. Performance = Safety, traffic laws.
    

---

To answer your side question about the self-driving car: **It is operating in a Multi-Agent environment.**  
The other entities do **not** have to be other self-driving cars. In AI, anything that perceives its environment and acts upon it to achieve its goals can be considered an agent. Therefore, human drivers, pedestrians, cyclists, and even traffic lights (if they are smart/adaptive) are all considered independent agents. Because the self-driving car has to coordinate, predict, and react to the independent behaviors of all these other entities, the environment is highly multi-agent.