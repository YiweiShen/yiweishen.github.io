title: Code Analysis for Applying MVC
date: 2015-11-15 13:29:52
tags: swift
---

For the code in the Stanford iOS 8 lession 3 Applying MVC, I try to comment on the CalculatorBrain.swift line by line.  Some of my thoughts might be naive.  Please bear with me.

```
import Foundation
//necessary to import this

class CalculatorBrain {
//define a class without inherit from any objective-c class
    
    private enum Op {
    //define a private enum
        case Operand(Double)  
        //for the numbers may be entered
        case Unaryoperation(String, Double -> Double)  
        //for the operation such as sqrt
        case Binaryoperation(String, (Double,Double) -> Double)  
        //for the operation such as plus or minus

        var description: String {  
        //define a read-only string for enum values
            get {  
            //without set so this is read-only
                switch self {  
                //from each enum value itself to figure out the description for each one
                case .Operand(let operand):
                    return "\(operand)"  
                    //in case of numbers, use the number as description
                case .Unaryoperation(let symbol, _):
                    return symbol
                case .Binaryoperation(let symbol, _):
                    return symbol  
                    //in case of operations, use the symbol as description string, _ just means that we dont care for that
                }
            }
        }
}
    
    private var opStack = [Op]()
    //define the opStack for store the numbers or operation symbols as an array
    
    private var knownOps = [String: Op]()
    //define the knownOps for known operations in dictionary for later use
        
    init () {  
    //here initiate for the knownOps dictionary
        knownOps["✕"] = Op.Binaryoperation("✕",*)  
        //* is the build-in operating function that does (Double,Double) -> Double
        knownOps["÷"] = Op.Binaryoperation("÷") { $0 / $1 }  
        //if the func is the last parameter, then it is legit to leave outside like this
        knownOps["+"] = Op.Binaryoperation("+",+)  
        //similar to "x"
        knownOps["−"] = Op.Binaryoperation("−") { $0 - $1 }  
        //also $0 refers to the first operand when passed in, $1 for the second
        knownOps["√"] = Op.Unaryoperation("√", sqrt)
    }  //for example, knownOps["x"] would be "x" : "x", *
    
    private func evaluate(ops:[Op]) -> (result:Double?, remainingOps:[Op]) {  
    //define a private func named evaluate and takes ops as input and two output as result and remainingOps for iteration if necessary
        if !ops.isEmpty {  
        //only when ops is not empty
            var remainingOps = ops  
            //for the purpose of manipulating the send-in parameter ops, otherwise it is just constant copy of ops
            let op = remainingOps.removeLast()  
            //then we really removed the last item in ops and return the last item value to op for next swith process
            switch op {  
            //swith has to look after every possibility, or you need a default case
            case .Operand(let operand):
                return (operand, remainingOps)  
                //in case of number, return a tuple (the number, and the remaining opStack), quite descriptive
            case .Unaryoperation(_, let operation):  
            //get the certain operation
                let operandEvaluation = evaluate(remainingOps)  
                //try iteration
                if let operand = operandEvaluation.result {  
                //only if iteration comes back with the result
                return (operation(operand),operandEvaluation.remainingOps)  
                //then the operation of the result is returned as first parameter and remaining Ops of the operandEvaluation as the second
                }
            case .Binaryoperation(_, let operation):  
            //not so triky if take a deep look
                let operandEvaluation = evaluate(remainingOps)
                if let operand1 = operandEvaluation.result {  
                //because it is binary operation which means it need two operands, how to get them, by two .result from twice operandEvaluation
                    let operandEvaluation = evaluate(remainingOps)
                    if let operand2 = operandEvaluation.result {  
                    //get the second operand
                        return (operation(operand1,operand2),operandEvaluation.remainingOps)
                        //perform the binary operation, return the result as the first parameter and the remaining opStack for further handling
                    }
                }
            }
        }
        return (nil, ops)  
        //if ops is empty, return nil and ops which is empty
    }
    
    func evaluate() -> Double? {  
    //only in the swift, we can overload function with the same name
        let (result, _) = evaluate(opStack)  
        //you see, actually we are doing the evaluate(opStack)
        return result  
        //and only return the result of it
    }
    
    func pushOperand(operand:Double) -> Double? {  
    //pass in the number and will pass out the number
        opStack.append(Op.Operand(operand))  
        //append the number to opStack
        return evaluate()  
        //result is the number
    }
    
    func performOperation(symbol:String) -> Double? {  
    //pass in the operation symbol and will pass out the operation result if it could
        if let operation = knownOps[symbol] {  
        //check if the operation is known
            opStack.append(operation)  
            //if the symbol is known then add to opStack
        }
        return evaluate()  
        //try to return of the known operation
    }

}
```