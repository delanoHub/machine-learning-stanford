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
    
<img src="img/ploat1.png" alt="Ploat Data">

### Compute Cost Function

<img src="img/costFunction.png" alt="Cost Fuction">

    function J = computeCost(X, y, theta)
    
        m = length(y); % number of training examples
        J = 1/(2*m)*sum((X*theta-y).^2); 
        
    end

### Gradient Descent

<img src="img/gradientdescent.png" alt="Gradient Descent">

    function [theta, J_history] = gradientDescent(X, y, theta, alpha, num_iters)

        m = length(y); % number of training examples
        J_history = zeros(num_iters, 1);

        for iter = 1:num_iters
        
            theta=theta-(alpha/m)*((X*theta-y)'*X)';

            % Save the cost J in every iteration    
            J_history(iter) = computeCost(X, y, theta);

        end

    end
    
### Gradient Descent - Non-vectorized 

    function [theta, J_history] = gradientDescent2(X, y, theta, alpha, num_iters)

    % Initialize some useful values

    m = length(y); % number of training examples
    J_history = zeros(num_iters, 1);

    theta1 = theta(1);
    theta2 = theta(2);

    temp0 = 0;
    temp1 = 0;
    error = 0;

    for iter = 1:(num_iters)
    
        h = X * theta; %heres the variable i moved into the loop

        temp0 = 0;
        temp1 = 0;

        for i=1:m
            error = (h(i) - y(i));
            temp0 = temp0 + (error * X(i, 1));
            temp1 = temp1 + (error * X(i, 2));
            %disp(error);
        end

        theta1 = theta1 - ((alpha/m) * temp0)
        theta2 = theta2 - ((alpha/m) * temp1)
        theta = [theta1;theta2];

        J_history(iter) = computeCost(X, y, theta);

    end
    end
    
 ## Prediction
 
    X = [ones(m, 1), data(:,1)]; % Add a column of ones to x
    theta = zeros(2, 1); % initialize fitting parameters

    % Some gradient descent settings
    iterations = 1500;
    alpha = 0.01;

    fprintf('\nTesting the cost function ...\n')
    % compute and display initial cost
    J = computeCost(X, y, theta);
    fprintf('With theta = [0 ; 0]\nCost computed = %f\n', J);
    fprintf('Expected cost value (approx) 32.07\n');

    % further testing of the cost function
    J = computeCost(X, y, [-1 ; 2]);
    fprintf('\nWith theta = [-1 ; 2]\nCost computed = %f\n', J);
    fprintf('Expected cost value (approx) 54.24\n');

    fprintf('Program paused. Press enter to continue.\n');
    pause;

    fprintf('\nRunning Gradient Descent ...\n')
    % run gradient descent
    theta = gradientDescent(X, y, theta, alpha, iterations);

### Gradient Descent - Non-vectorized 

    % print theta to screen
    fprintf('Theta found by gradient descent:\n');
    fprintf('%f\n', theta);
    fprintf('Expected theta values (approx)\n');
    fprintf(' -3.6303\n  1.1664\n\n');

    % Plot the linear fit
    hold on; % keep previous plot visible
    plot(X(:,2), X*theta, '-')
    legend('Training data', 'Linear regression')
    hold off % don't overlay any more plots on this figure

    % Predict values for population sizes of 35,000 and 70,000
    predict1 = [1, 3.5] *theta;
    fprintf('For population = 35,000, we predict a profit of %f\n',...
        predict1*10000);
    predict2 = [1, 7] * theta;
    fprintf('For population = 70,000, we predict a profit of %f\n',...
        predict2*10000);

    fprintf('Program paused. Press enter to continue.\n');
    pause;


    Theta found by gradient descent:  
    -3.630291  
    1.166362  



For population = 35,000, we predict a profit of 4519.767868  
For population = 70,000, we predict a profit of 45342.450129  

<img src="img/ploat2.png" alt="Ploat Data">

