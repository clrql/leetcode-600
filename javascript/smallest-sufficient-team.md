
  # smallest-sufficient-team

  ```javascript
  /**
 * @param {string[]} req_skills
 * @param {string[][]} people
 * @return {number[]}
 */
var smallestSufficientTeam = function(req_skills, people) {
  const n = req_skills.length;
  const skillMap = new Map();
  
  // Map skills to their corresponding bitmask value
  for (let i = 0; i < n; i++) {
    skillMap.set(req_skills[i], i);
  }
  
  const dp = new Array(1 << n).fill(Infinity); // Minimum team size for each bitmask
  dp[0] = 0; // Base case: no skills required
  
  const team = new Array(1 << n).fill([]);
  
  // Iterate over each person and update the dp array
  for (let i = 0; i < people.length; i++) {
    const personSkills = people[i];
    let bitmask = 0; // Bitmask representing skills possessed by the person
    
    // Calculate the bitmask for the person's skills
    for (let j = 0; j < personSkills.length; j++) {
      const skill = personSkills[j];
      if (skillMap.has(skill)) {
        const skillIndex = skillMap.get(skill);
        bitmask |= (1 << skillIndex); // Set the bit representing the skill
      }
    }
    
    // Update the dp array based on the current person
    for (let prevBitmask = 0; prevBitmask < (1 << n); prevBitmask++) {
      if (dp[prevBitmask] + 1 < dp[prevBitmask | bitmask]) {
        dp[prevBitmask | bitmask] = dp[prevBitmask] + 1;
        team[prevBitmask | bitmask] = [...team[prevBitmask], i];
      }
    }
  }
  
  return team[(1 << n) - 1]; // Return the team for the bitmask representing all required skills
};

  ```
  