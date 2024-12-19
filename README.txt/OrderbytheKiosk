const kioskOrderMachine= () => {
    // Sellers' authentication data
    const sellers = [
        { username: "admin", password: "amandacute24" },
        { username: "seller", password: "uttotka70" }
    ];

    // Categories and items storage
    const categories = {
        Pasta: [
            { name: "Spaghetti", price: 120 },
            { name: "Carbonara", price: 150 },
            { name: "Lasagna", price: 500 },
            { name: "Macaroni", price: 110 }
        ],
        Desserts: [
            { name: "Halo Halo", price: 120 },
            { name: "Ice Cream", price: 120 },
            { name: "Cake", price: 500 },
            { name: "Brownie", price: 300 },
            { name: "Candy", price: 10 },
            { name: "Letche Plan", price: 350 },
            { name: "Maja BLanca", price: 100 }
        ],
        Drinks: [
            { name: "Soda", price: 70 },
            { name: "Juice", price: 35 },
            { name: "Coffee", price: 70 },
            { name: "Soju", price: 360 },
            { name: "2by2" , price: 75 }
        ]
    };

    // Customer cart storage
    const cart = [];

    // Authenticate seller
    const authenticateSeller = (username, password) => {
        return sellers.some(seller => seller.username === username && seller.password === password);
    };

    // Add item to a category
    const addItem = (category, name, price) => {
        categories[category].push({ name, price });
    };

    // Remove item from a category
    const removeItem = (category, name) => {
        categories[category] = categories[category].filter(item => item.name !== name);
    };

    // Sort cart using Bubble Sort
    const sortCart = () => {
        for (let i = 0; i < cart.length - 1; i++) {
            for (let j = 0; j < cart.length - i - 1; j++) {
                if (cart[j].name > cart[j + 1].name) {
                    [cart[j], cart[j + 1]] = [cart[j + 1], cart[j]];
                }
            }
        }
    };

    // Customer actions
    const customerActions = () => {
        while (true) {
            const action = prompt("What would you like to do? (ORDER, VIEW CART, CANCEL)");

            if (action === "ORDER") {
                const category = prompt("Choose a category: Pasta, Desserts, Drinks");
                if (!categories[category]) {
                    console.log("Sorry, that category doesn’t exist. Please try again.");
                    continue;
                }

                const itemName = prompt("Enter the name of the item you'd like to order:");
                const item = categories[category].find(item => item.name === itemName);

                if (!item) {
                    console.log("Sorry, we don’t have that item. Please try again.");
                    continue;
                }

                const quantity = parseInt(prompt("How many would you like to order?"), 10);
                if (isNaN(quantity) || quantity <= 0) {
                    console.log("Please enter a valid quantity.");
                    continue;
                }

                cart.push({ ...item, quantity });
                console.log(`${quantity} x ${item.name} added to your cart.`);

            } else if (action === "VIEW CART") {
                if (cart.length === 0) {
                    console.log("Your cart is empty.");
                } else {
                    const cartAction = prompt("What would you like to do? (PRINT CART, ADD MORE, REMOVE ITEM, CANCEL)");

                    if (cartAction === "PRINT CART") {
                        sortCart();
                        console.log("Here’s what’s in your cart:");
                        cart.forEach(item => {
                            console.log(`Item: ${item.name}, Price: $${item.price.toFixed(2)}, Quantity: ${item.quantity}, Total: $${(item.price * item.quantity).toFixed(2)}`);
                        });
                    } else if (cartAction === "REMOVE ITEM") {
                        const itemName = prompt("Enter the name of the item you want to remove:");
                        const index = cart.findIndex(item => item.name === itemName);

                        if (index > -1) {
                            cart.splice(index, 1);
                            console.log(`${itemName} has been removed from your cart.`);
                        } else {
                            console.log("That item is not in your cart.");
                        }
                    } else if (cartAction === "CANCEL") {
                        break;
                    }
                }

            } else if (action === "CANCEL") {
                break;
            } else {
                console.log("Invalid choice. Please try again.");
            }
        }
    };

    // Seller actions
    const sellerActions = () => {
        while (true) {
            const action = prompt("What would you like to do? (LOGOUT, ADD ITEM, REMOVE ITEM)");

            if (action === "LOGOUT") {
                console.log("Logging out. Have a great day!");
                break;

            } else if (action === "ADD ITEM") {
                const category = prompt("Which category would you like to add to? (Pasta, Desserts, Drinks)");
                if (!categories[category]) {
                    console.log("That category doesn’t exist. Please try again.");
                    continue;
                }

                const name = prompt("Enter the name of the item:");
                const price = parseFloat(prompt("Enter the price of the item:"));

                if (isNaN(price) || price <= 0) {
                    console.log("Please enter a valid price.");
                    continue;
                }

                addItem(category, name, price);
                console.log(`${name} has been added to the ${category} category.`);

                const continueAdding = prompt("Would you like to add another item? (YES/NO)");
                if (continueAdding !== "YES") break;

            } else if (action === "REMOVE ITEM") {
                const category = prompt("Which category would you like to remove from? (Pasta, Desserts, Drinks)");
                if (!categories[category]) {
                    console.log("That category doesn’t exist. Please try again.");
                    continue;
                }

                const name = prompt("Enter the name of the item to remove:");
                removeItem(category, name);
                console.log(`${name} has been removed from the ${category} category.`);

                const continueRemoving = prompt("Would you like to remove another item? (YES/NO)");
                if (continueRemoving !== "YES") break;

            } else {
                console.log("Invalid choice. Please try again.");
            }
        }
    };

    // Main system loop
    while (true) {
        const role = prompt("Are you a SELLER or a CUSTOMER?");

        if (role === "SELLER") {
            const username = prompt("Please enter your username:");
            const password = prompt("Please enter your password:");

            if (authenticateSeller(username, password)) {
                console.log("Welcome back!");
                sellerActions();
            } else {
                console.log("Invalid username or password. Please try again.");
            }

        } else if (role === "CUSTOMER") {
            console.log("Welcome! Let’s place your order.");
            customerActions();

        } else {
            console.log("Invalid role. Please enter either SELLER or CUSTOMER.");
        }
    }
};

kioskOrderMachine();
