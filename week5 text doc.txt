class Car {
    constructor(name,style){

        this.name = name;
        this.style = style;
    }

    description () {
        return `this car's name is $${this.name} and its style is ${this.style}`;
    }
}



class LotSection {
    constructor(name) {
        this.name = name;
        this.cars = [];
    }
    addCar(car){
        if (car instanceof Car){
            this.cars.push(car);
        } else {
            throw new Error("we can only add a car");
        }
    }
    describe(){
        return `${this.name} has ${this.cars}`;
    }
}

class Menu {
    constructor(){
        this.lotsections = [];
        this.selectedLot = null;
    }
    start() {
        let selection = this.showMain();
        while (selection != 0) {
switch (selection){
    case '1' : this.createLot();
    break;
    case '2' : this.viewLot();
    break;
    case '3': this.deleteLot();
    break;
    case '4': this.displayLots();
    break;
    default:
        selection = 0;
}
selection = this.showMain();
        }
        alert('Application Terminated');
 
    }
    showMain() {
        return prompt(`
        Car location Tracker Menu
        0 exit
        1 build lot
        2 view lot
        3 delete lot
        4 display all Lots
        
        
        `);
    }

    lotMenu(carInfo){
        return prompt(` 
        0) back
        1) create car
        2) delete car
        ----
        ${carInfo}
        `);
    }

    displayLots() {
        let string = '';
        for (let i = 0; i < this.lotsections.length; i++) {
            string += i+ ")" + this.lotsections[i].name + '\n';
        }
        alert(string);
    }
    createLot() {
        let name = prompt('enter name for lot');
        this.lotsections.push( new LotSection(name));
    }

    viewLot() {
        let index = prompt(" enter lot number");
        if (index > -1 && index < this.lotsections.length) {
            this.selectedLot = this.lotsections[index];
            let description = " Lot name : " + this.selectedLot.name + "\n";
            for ( let i = 0; i < this.selectedLot.cars.length; i++) {
                description += i + ')' + this.selectedLot.cars[i].name
                 + '-' + this.selectedLot.cars[i].style + '\n';
            }
            let selection1 = this.lotMenu(description)
            switch (selection1) {
                case '1': this.createCar();
                break; 
                case '2' : this.deleteCar();
            }

        }
        }

        deleteLot(){
            let index = prompt("enter index of lot to deleate");
            if (index > -1 && index < this.lotsections.length){
                this.lotsections.splice(index,1);
            }
        }
        createCar(){
            let name = prompt("enter car name");
            let style = prompt("enter style, ie sedan, suv, truck, van");
            this.selectedLot.cars.push(new Car(name,style));
        }

        deleteCar() {
            let index = prompt("enter index to delete car");
            if (index > -1 && index < this.selectedLot.cars.length) {
                this.selectedLot.cars.splice(index, 1);
            }
        }

    }


let menu = new Menu();
menu.start();








