---
title: Simulations and Implementations
parent: Short Rate Models
nav_order: 2
---
## Short Rate Models

### Vasicek
```python
class ShortRate(): 
    # Generate Short Rates using Monte Carlo Simulation 

    def __init__(self, rt, t, T, dt, theta, kappa, sigma): 

        # Read in time length you want to predict 
        self.rt = rt 
        self.t = t
        self.T = T 
        self.dt = dt 
        self.theta = theta 
        self.kappa = kappa 
        self.sigma = sigma 
    
    def Vasicek(self): 

        # Simulate 1 path of short rate under Vasicek design 
        path_length = int((self.T-self.t)/self.dt) 
        Z = np.random.normal(0.0, 1.0, size=path_length) 

        rate_path = np.zeros(path_length+1) 
        rate_path[0] = self.rt 

        var = self.sigma**2/(2*self.kappa)*(1-np.exp(-2*self.kappa*self.dt)) 
        rate_path[1:] = np.sqrt(var)*Z 

        for i in range(1, len(rate_path)): 
            rate_path[i] = rate_path[i-1]*np.exp (-self.kappa*self.dt)+self.theta*(1-np.exp(-self.kappa*self.dt))

        return rate_path 

    def HullWhite(self): 

        # Simulate 1 path of short rate under Hull White 
        path_length = int(self.T) 
        Z = np.random.normal(0.0, 1.0, size=path_length) 

        rate_path = np.zeros(path_length+1) 
        
    
    def HoLee(self): 

        # Simulate 1 path of short rate under Ho-Lee 
        path_length = int(self.T) 
        Z = np.random.normal(0.0, 1.0, size=path_length) 

        rate_path = np.zeros(path_length+1) 

    def CIR(self): 

        # Simulate 1 path of short rate under CIR 
        path_length = int(self.T) 
        Z = np.random.normal(0.0, 1.0, size=path_length) 

        rate_path = np.zeros(path_length+1) 

    def mc_short_rate(self, n_trials=10000): 

        # Monte Carlo Simulation for Short Rate 
        simulation = pd.DataFrame() 

        for _ in range(n_trials): 
            simulation.loc[:, _] = self.Vasicek() 

        for _ in range(n_trials): 
            simulation.loc[:, _] = self.HullWhite() 
        
        for _ in range(n_trials): 
            simulation.loc[:, _] = self.HoLee() 

        for _ in range(n_trials): 
            simulation.loc[:, _] = self.CIR() 

        return 
```
