# Code Review: TICKET-101

## Task Overview
Please design a decision engine which takes in personal code, loan amount, loan period in months
and returns a decision (negative or positive) and the amount.
The idea of the decision engine is to determine what would be the maximum sum, regardless of the
person requested loan amount. For example if a person applies for €4000,-, but we determine that
we would approve a larger sum then the result should be the maximum sum which we would
approve.

Also, in reverse, if a person applies for €4000,- and we would not approve it then we want to return
the largest sum which we would approve, for example €2500,-,. If a suitable loan amount is not
found within the selected period, the decision engine should also try to find a new suitable period. In
real life the solution should connect to external registries and compose a comprehensive user
profile, but for the sake of simplicity this part can be mocked as a hard coded result for certain
personal codes.


## Reviewer
- **Name:** Danil Zimarev
- **Date:** 18.04.2024


## Functionality
- **Completeness:**
    - The requirements were partially implemented as the solution does not take customer credit score into account.
- **Correctness:**
    - Code is well-structured and readable, maintaining consistent style.


## Testing
- Integrated tests cover tasks basics, and all DecisionEngine tests pass.


## Documentation
- **Code Comments:**
    - The code has solid commenting - all methods have enough explanation to understand their purpose.

## Suggestions for improvement

FRONT-END
---------

1. **State management:** 
   - As the UI uses sliders to get new values from the customer, it is inefficient to use simple state
   management like setState() each time a new value comes. If the user is sliding the slider back and forth, it could
   result in an enormous amount of unnecessary server requests. Consider optimizing server requests by updating state 
   at intervals, rather than with every slider movement
   
2. Simplify loan_form widget for easier understanding, possibly dividing it into two widgets.

BACK-END
---------

1. One requirement is for the decision engine to return the maximum possible loan sum for the requested period,
   even if the used input is less. Currently, it just calculates the sum that is equal or less than requested.
2. The ticket requires implementing a scoring algorithm to calculate customer's credit score. This solution has not
   been implemented (to be used for point No. 1).
3. Provide explanation for unsuccessful loan requests, especially for customers in debt.

To fix this shortcoming

- Implemented calculateCustomerCreditScore() method to calculate customer's credit score
- Used this method to determine the highest valid loan amount based on credit score.
- Adjusted loan amount based on credit score, ensuring approval within acceptable limits.

## Summary
The DecisionEngine demonstrates strong code organization and user-friendly design. However, it lacks crucial functionality
regarding maximum loan calculation and credit score assessment, impacting lending decisions. Improvements are necessary 
in algorithmic calculations, state management, and credit scoring implementation to fulfill requirements effectively.