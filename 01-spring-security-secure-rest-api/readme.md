#

```java
package com.example.config;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.http.HttpMethod;
import org.springframework.security.authentication.AuthenticationManager;
import org.springframework.security.config.annotation.authentication.builders.AuthenticationManagerBuilder;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;
import org.springframework.security.web.SecurityFilterChain;
import org.springframework.security.web.util.matcher.AntPathRequestMatcher;

@Configuration
public class WebSecurityConfig {
    @Bean
    public BCryptPasswordEncoder bCryptPasswordEncoder() {
        return new BCryptPasswordEncoder();
    }

    @Bean
    SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
        http.httpBasic();
        http.authorizeHttpRequests()
                //.requestMatchers(new AntPathRequestMatcher("/couponapi/coupons/**", HttpMethod.GET.name()))
                .requestMatchers(new AntPathRequestMatcher("/couponapi/coupons/{code:^[A-Z]*$}", HttpMethod.GET.name()))
                .hasAnyRole("USER", "ADMIN")
                .requestMatchers(new AntPathRequestMatcher("/couponapi/coupons/", HttpMethod.POST.name()))
                .hasAnyRole("ADMIN")
                .and()
                .csrf()
                .disable();

        return http.build();
    }

    @Bean
    public AuthenticationManager authenticationManager(HttpSecurity http) throws Exception {
        return http.getSharedObject(AuthenticationManagerBuilder.class)
                .build();
    }
}
```
