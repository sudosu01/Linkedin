# Linkedin

Linkedin-autofollower.
This script follows linkedin users automatically.

> Go to https://linkedin.com/in/YOUR_USER_NAME/

> Navigate to the search field and configure the filter option to any region

> Open the Developer Console. (COMMAND+ALT+I on Mac) | (COMMAND+SHIFT+I on Windows)

> Paste the below code into the Developer Console and run it


      // Ensure you're on a LinkedIn search page with results loaded
      let followCount = 0;
      let maxFollow = 100; // The max number of profiles to follow at once
      
      function followProfiles() {
        // Find all 'connect' buttons and 'follow' buttons on the page
        let connectButtons = document.querySelectorAll('button.artdeco-button');
        let followButtons = document.querySelectorAll('button[aria-label="Follow"]');
      
        // Create an array of button elements that are connect/follow buttons
        let allButtons = [...connectButtons, ...followButtons];
        
        allButtons.forEach((button) => {
          if (followCount >= maxFollow) return; // Stop after maxFollow
          try {
            button.click(); // Click the button to follow/connect
            followCount++;
            console.log(`Followed: ${followCount}`);
          } catch (err) {
            console.log('Error following user: ', err);
          }
        });
      
        if (followCount < maxFollow) {
          // If we haven't reached the limit, scroll to load more profiles
          window.scrollBy(0, window.innerHeight);
          setTimeout(followProfiles, 2000); // Wait 2 seconds before trying again
        } else {
          console.log(`Finished following ${followCount} profiles.`);
        }
      }
      
      // Start following
      followProfiles();
