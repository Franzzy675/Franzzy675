document.addEventListener('DOMContentLoaded', () => {
    const playerHealthElem = document.getElementById('player-health');
    const enemyHealthElem = document.getElementById('enemy-health');
    const messageElem = document.getElementById('message');
    const attackButton = document.getElementById('attack');
    const healButton = document.getElementById('heal');
    
    let playerHealth = 100;
    let enemyHealth = 100;
    const playerAttack = 10;
    const enemyAttack = 10;

    function updateHealth() {
        playerHealthElem.textContent = playerHealth;
        enemyHealthElem.textContent = enemyHealth;
    }

    function checkGameOver() {
        if (playerHealth <= 0) {
            messageElem.textContent = 'You have been defeated!';
            attackButton.disabled = true;
            healButton.disabled = true;
        } else if (enemyHealth <= 0) {
            messageElem.textContent = 'You have won the battle!';
            attackButton.disabled = true;
            healButton.disabled = true;
        }
    }

    attackButton.addEventListener('click', () => {
        if (enemyHealth > 0) {
            enemyHealth -= playerAttack;
            if (enemyHealth > 0) {
                playerHealth -= enemyAttack;
            }
            updateHealth();
            checkGameOver();
        }
    });

    healButton.addEventListener('click', () => {
        if (playerHealth > 0 && enemyHealth > 0) {
            playerHealth += 10;
            playerHealth = Math.min(playerHealth, 100); // Cap health at 100
            playerHealth -= enemyAttack;
            if (playerHealth <= 0) {
                playerHealth = 0;
            }
            updateHealth();
            checkGameOver();
        }
    });

    updateHealth();
});
