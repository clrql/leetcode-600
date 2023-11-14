
  # defanging-an-ip-address

  ```javascript
  /**
 * @param {string} address
 * @return {string}
 */
var defangIPaddr = function(address) {
    return address.replaceAll(".", "[.]");
};
  ```
  