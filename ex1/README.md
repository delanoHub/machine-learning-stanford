# Programming Exercise 1: Linear Regression

### WarmUpExercise
    function A = warmUpExercise()
    
        A = [];
        A = eye(5);
     
     end

Return a 5 x 5 identity matrix.

1   &nbsp;&nbsp;&nbsp;0   &nbsp;&nbsp;&nbsp;0   &nbsp;&nbsp;&nbsp;0   &nbsp;&nbsp;&nbsp;0  
0   &nbsp;&nbsp;&nbsp;1   &nbsp;&nbsp;&nbsp;0   &nbsp;&nbsp;&nbsp;0   &nbsp;&nbsp;&nbsp;0  
0   &nbsp;&nbsp;&nbsp;0   &nbsp;&nbsp;&nbsp;1   &nbsp;&nbsp;&nbsp;0   &nbsp;&nbsp;&nbsp;0  
0   &nbsp;&nbsp;&nbsp;0   &nbsp;&nbsp;&nbsp;0   &nbsp;&nbsp;&nbsp;1   &nbsp;&nbsp;&nbsp;0  
0   &nbsp;&nbsp;&nbsp;0   &nbsp;&nbsp;&nbsp;0   &nbsp;&nbsp;&nbsp;0   &nbsp;&nbsp;&nbsp;1  

### Load the Data

    data = load('ex1data1.txt');
    X = data(:, 1); 
    y = data(:, 2);
    m = length(y); % number of training examples
    
### Plotting the Data

    function plotData(x, y) 
    
        figure; % open a new figure window
        plot(x, y, 'rx', 'MarkerSize', 10); % Plot the data
        ylabel('Profit in $10,000s'); % Set the y?axis label
        xlabel('Population of City in 10,000s'); % Set the x?axis label
        
    end
    
<img src="ploat1.png" alt="Ploat Data">
    

