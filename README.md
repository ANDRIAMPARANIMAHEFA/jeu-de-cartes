const prompt = require("prompt-sync")();

console.log("\n  \n          Veillez patienter lors du chargement ... \n   ");
console.log("::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::");
console.log("!!                                                        ??");
console.log("!!                                                        ??");
console.log("::         😊 Bienvenue dans le jeu du carte 😊           ::");
console.log("!!                                                        ??");
console.log("!!                                                        ??");
console.log(":::::::::::::::::::::::::::::::::::::::::::::::::::::::::::: \n");
console.log("  ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~");
console.log("      - Taper 1 pour Jouer. \n         - Taper 2 pour quitter le jeu.");
console.log("  ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~");

let choix = +prompt("Faites votre choix : ");

if (choix === 1) {
    jouerAuJeu();
} else if (choix === 2) {
    console.log("Merci d'avoir visité !!");
}

function jouerAuJeu() 
{
    let pseudoDuJoueur = prompt("Saisir votre pseudo : ");
    console.log("Bienvenue dans le jeu de cartes!");
    console.log(`Bienvenue, ${pseudoDuJoueur}! Le jeu commence!\n`);

    let typesCartes = ["EAU", "FEU", "PLANTE"];
    let victoire = 0;

    for (let tour = 1; tour <= 3; tour++) 
    {
        console.log(`C'est le tour numéro ${tour}.`);

        let carteDuJoueur = prompt("Choisissez une carte (EAU, FEU, PLANTE) : ").toUpperCase();
        let carteDuRobot = choisirCarte(typesCartes);

        console.log(`${pseudoDuJoueur}, vous avez choisi la carte ${carteDuJoueur}.`);
        console.log(`Le robot choisit la carte ${carteDuRobot}.\n`);

        let resultatManche = determinerLeResultat(carteDuJoueur, carteDuRobot);

        console.log(`Le résultat du tour est : ${resultatManche}\n`);

        if (resultatManche === "Victoire") {
            victoire++;
        }
    }

    console.log("\nRésultat final :");
    if (victoire > 1) 
    {
        console.log(`Félicitations, ${pseudoDuJoueur}! Vous avez remporté le jeu!\n`);
        relancerJeu();
    } 
    else if (victoire === 1) 
    {
        console.log(`${pseudoDuJoueur}, vous avez gagné une manche sur trois. Essayez encore!\n`);
        relancerJeu();
    }
    else 
    {
        console.log(`${pseudoDuJoueur}, c'est une défaite. Essayez encore!\n`);
        relancerJeu();
    }
}
    
function choisirCarte(typesCartes) 
{
    const choix = Math.floor(Math.random() * typesCartes.length);
    return typesCartes[choix];
}
    
function determinerLeResultat(carteDuJoueur, carteDuRobot) 
{
    if (
        (carteDuJoueur === "EAU" && carteDuRobot === "FEU") ||
        (carteDuJoueur === "FEU" && carteDuRobot === "PLANTE") ||
        (carteDuJoueur === "PLANTE" && carteDuRobot === "EAU")
    ) 
    {
        return "Victoire";
    } 
    else if (carteDuJoueur === carteDuRobot) {
        return "Égalité";
    } 
    else 
    {
        return "Défaite";
        
    }
}
    
function relancerJeu() 
{
    let question = prompt("Voulez-vous retenter votre chance contre le robot ? (oui/non) : ")
    if (question === "oui") 
    {
        jouerAuJeu();
    }
    else 
    {
        console.log("Merci d'avoir joué! À bientôt.");
    }
}  
    



   
