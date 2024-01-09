import inquirer from "inquirer";

interface ansType {
    userId: string;
    userPin: number;
    AccountType: string;
    TransactionType: string;
    amount?: number;
    withDrawaMethod?: number;
}


const answers: ansType = await inquirer.prompt([
    {
        type: "input",
        name: "userId",
        message: "Kindly Enter Your Id",
    },
    {
        type: "number",
        name: "userPin",
        message: "Kindly Enter Your Pin",
    },
    {
        type: "list",
        name: "AccountType",
        choices: ["Current", "Saving"],
        message: "Select Your Account Type",
    },
    {
        type: "list",
        name: "TransactionType",
        choices: ["Fast Cash", "Withdraw"],
        message: "Select Your Transaction Type",
        when: (answers) => answers.AccountType === "Current" || answers.AccountType === "Saving",
    },
    {
        type: "list",
        name: "withDrawaMethod",
        choices: [1000, 2000, 10000, 25000],
        message: "Select Your Amount",
        when: (answers) => answers.TransactionType === "Fast Cash",
    },
    {
        type: "number",
        name: "amount",
        message: "Enter Your Amount",
        when: (answers) => answers.TransactionType === "Withdraw",
    },
]);

if (answers.userId && answers.userPin) {
    const balance = Math.floor(Math.random() * 1000000);
    console.log("Your Current Balance Is", balance);

    const EnteredAmount = answers.amount || answers.withDrawaMethod || 0;

    if (balance >= EnteredAmount) {
        const remaining = balance - EnteredAmount;
        console.log("Your Remaining Balance Is", remaining);
    } else {
        console.log("Insufficient Balance");
    }
}
