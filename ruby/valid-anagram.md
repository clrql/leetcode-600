
  # valid-anagram

  ```ruby
  # @param {String} s
# @param {String} t
# @return {Boolean}
def is_anagram(s, t)
    return false if s.length != t.length
    
    s_count = Hash.new(0)
    t_count = Hash.new(0)

    s.each_char { |char| s_count[char] += 1}
    t.each_char { |char| t_count[char] += 1}

    return s_count == t_count
end
  ```
  