# Hydraulic-Structure-Dimension-Calculator
This Python automation script calculates the dimensions for Free Hydraulic Jump, USBR Type III Stilling Basins, USBR Type IV Stilling Basins, Saint Anthony Falls (SAF) Stilling Basins and Straight Drop Structures.

###### Please Visit https://consultme2.wixsite.com/pythonscripts for more information, tutorial video and more python scripts.

## Stilling Basin with Free Hydraulic Jump
Example of Stilling Basin with Free Hydraulic Jump Dimensions:
Froude Number - 4.8 (min), 19.6 (max) | Required Tailwater^3, m/ft - 3.1/10.1 | Basin Length, m/ft - 33.7/109.2 | Basin Depth, m/ft - 4.8/15.5

A hydraulic structure that is used in dam spillways and other water control systems. It's designed to dissipate the energy of rapidly flowing water, preventing erosion downstream. When high-velocity water enters the basin, it forms a turbulent jump, slowing down and converting kinetic energy into heat and turbulence. This process prevents erosion and ensures a safe and controlled release of water, safeguarding the stability of the surrounding area.

### USER INPUT
 - Discharge (cms);
 - Channel Width (B) (m) of Income Channel;
 - Longitudinal Slope (So) (m/m) of Income Channel;
 - Manning's Roughness (n) of Income Channel;
 - Ratio of tailwater to conjugate depth (TW/y2);
 - Ground elevation at the Incoming channel outlet (m);
 - Width of the basin (m/s);
 - Slope leaving the basin (m/m);
 - Slope of the transition entering the basin (m/m);
 - Longitudinal Slope (So) (m/m) of Outgoing Channel;
 - Mannings Roughness (n) of Outgoing Channel;
 - Channel Width (B) (m) of Outgoing Channel.

### STEP 1
Incoming Channel Brink Depth (y_0), Velocity (v_0) and Froude Number (fr_0) are determined.
Using the following equation: Q = (1/n) * ((A**(5/3)) / (P**(2/3))) * (S0**(1/2)), y_0 is calculated;
Using the following equation: Q / b*y, v_0 is calculated;
Using the following equation: v_0 / (sqrt(9.8*y_0)), fr_0 is calculated.

### STEP 2
Velocity (v_n) and Tail Water Depth (y_n_tw) in the receiving Channel Downstream of the Basin are determined.
Using the following equation: Q = (1/n) * ((A**(5/3)) / (P**(2/3))) * (S0**(1/2)), y_n_tw is calculated;
Using the following equation: Q / b*y, v_n is calculated.

### STEP 3
The Conjugate Depth for the income Channel Outlet Conditions is determined.
Using the following equation: ((c_income * y_0) / 2) * ((( 1 + (8*(fr_0**2)))**(1/2)) - 1), y_2_1 is calculated.
If y_2_1 > y_n_tw:
If y_2_1 ({y_2_1}) > TW ({y_n_tw}) a jump WILL NOT form and a basin is needed;
The process of Calculating Stilling Basin Dimensions will be continued below.
If y_2_1 <= y_n_tw:
Since y2 ({y_2_1}) <= TW ({y_n_tw}) a jump WILL form and a basin IS NOT needed.

### STEP 4
The length of the basin width is confirmed within acceptable limits.
Using the following equation: z_0 - (y_2_1 - y_n_tw), z_1 is calculated;
Using the following equation: (z_0 - z_1) / s_t, l_t is calculated.
Test: WB IS or IS NOT within acceptable limits:
Define test_wb as w_b + (((2*l_t) * (((s_t**2) + 1)**(1/2))) / (3 * fr_0));
If the Basin Width (w_b) is smaller (<) than or equal (=) to the test_wb, WB is within acceptable limits.
Using the following equation: Q = y_1 * w_b * ((((2 * 9.8) * (z_0 - z_1 + y_0 - y_1 )) + v_0²) ** (1/2)), y_1 is calculated;
Using the following equation: v_1 = Q / A, where A = y_1 * w_b, v_1 is calculated;
Using the following equation: (v_1) / ((9.8 * y_1)**(1/2)), fr_1 is calculated.

### STEP 5
Basin length and exit elevation are computed. Verify that sufficient tailwater exists to force the hydraulic jump.
Using the following equation: ((c_income * y_1) / 2) * ((( 1 + (8*(fr_1**2)))**(1/2)) - 1), y_2 is calculated;
Using the Length of Hydraulic Jump on a Horizontal Floor Graph, fr_1 is calculated;
Using the following equation: corresponding_lb_y2 * y_2, l_b is calculated;
Using the following equation: ((l_t * (s_t - s0_income)) - (l_b * s0_income)) / (s_s + s0_income), l_s is calculated;
Using the following equation: (l_s * s_s) + z_1, z_3 is calculated.
Test whether tailwater is sufficient to force a jump in the basin.
If y_2 (Conjugate depth for the culvert outlet) + z_1 (Ground elevation at the basin entrance) < z_3 (Elevation at the entrance to the tailwater channel) + y_n_tw (Tail Water Depth (m)), tailwater is sufficient to force a jump in the basin;
If Tailwater is not sufficient, change the ground elevation at the basin entrance (m) (z_1) so that y_2 + z_1 > z_3 + y_n_tw.

### STEP 6
The needed Radius of curvature for the slope changes entering the Basin is determined.
Using the following equation: y_0 / ((math.exp(1.5 / (fr_0 ** 2))) - 1), r_slope is calculated.

### STEP 7
The Basin Length is determined.
Using the following equation: l_t + l_b + l_s, basin_length is calculated.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## USBR Type III Stilling Basin
Example of USBR Type III Stilling Basin Dimensions: 
Froude Number - 4.5 (min), 17 (max) | Required Tailwater^3, m/ft - 3.0/9.6 | Basin Length, m/ft - 20.6/67.3 | Basin Depth, m/ft - 3.8/12.5

A USBR Type III Stilling Basin is a specialized hydraulic structure designed by the United States Bureau of Reclamation. It is utilized in dam projects to dissipate the energy of swiftly flowing water, preventing erosion and turbulence downstream. The basin features carefully positioned baffle blocks to break up the water's kinetic energy, coupled with a sloping concrete apron to further reduce velocity. The design aims to create a smooth transition between the basin and the natural channel, ensuring stable water flow as it exits the structure. USBR Type III Stilling Basins are meticulously engineered to safeguard riverbeds and banks, maintaining the integrity of water control systems.

### USER INPUT
 - Discharge (cms);
 - Channel Width (B) (m) of Income Channel;
 - Longitudinal Slope (So) (m/m) of Income Channel;
 - Manning's Roughness (n) of Income Channel;
 - Ratio of tailwater to conjugate depth (TW/y2);
 - Ground elevation at the Incoming channel outlet (m);
 - Width of the basin (m/s);
 - Slope leaving the basin (m/m);
 - Slope of the transition entering the basin (m/m);
 - Longitudinal Slope (So) (m/m) of Outgoing Channel;
 - Mannings Roughness (n) of Outgoing Channel;
 - Channel Width (B) (m) of Outgoing Channel.

### STEP 1
Incoming Channel Brink Depth (y_0), Velocity (v_0) and Froude Number (fr_0) are determined.
Using the following equation: Q = (1/n) * ((A**(5/3)) / (P**(2/3))) * (S0**(1/2)), y_0 is calculated;
Using the following equation: Q / b*y, v_0 is calculated;
Using the following equation: v_0 / (sqrt(9.8*y_0)), fr_0 is calculated.

### STEP 2
Velocity (v_n) and Tail Water Depth (y_n_tw) in the receiving Channel Downstream of the Basin are determined.
Using the following equation: Q = (1/n) * ((A**(5/3)) / (P**(2/3))) * (S0**(1/2)), y_n_tw is calculated;
Using the following equation: Q / b*y, v_n is calculated.

### STEP 3
The Conjugate Depth for the income Channel Outlet Conditions is determined.
Using the following equation: ((c_income * y_0) / 2) * ((( 1 + (8*(fr_0**2)))**(1/2)) - 1), y_2_1 is calculated.
If y_2_1 > y_n_tw:
If y_2_1 ({y_2_1}) > TW ({y_n_tw}) a jump WILL NOT form and a basin is needed;
The process of Calculating Stilling Basin Dimensions will be continued below.
If y_2_1 <= y_n_tw:
Since y2 ({y_2_1}) <= TW ({y_n_tw}) a jump WILL form and a basin IS NOT needed.

### STEP 4
The length of the basin width is confirmed within acceptable limits.
Using the following equation: z_0 - (y_2_1 - y_n_tw), z_1 is calculated;
Using the following equation: (z_0 - z_1) / s_t, l_t is calculated.
Test: WB IS or IS NOT within acceptable limits:
Define test_wb as w_b + (((2*l_t) * (((s_t**2) + 1)**(1/2))) / (3 * fr_0));
If the Basin Width (w_b) is smaller (<) than or equal (=) to the test_wb, WB is within acceptable limits.
Using the following equation: Q = y_1 * w_b * ((((2 * 9.8) * (z_0 - z_1 + y_0 - y_1 )) + v_0²) ** (1/2)), y_1 is calculated;
Using the following equation: v_1 = Q / A, where A = y_1 * w_b, v_1 is calculated;
Using the following equation: (v_1) / ((9.8 * y_1)**(1/2)), fr_1 is calculated.

### STEP 5
Basin length and exit elevation are computed. Verify that sufficient tailwater exists to force the hydraulic jump.
Using the following equation: ((c_income * y_1) / 2) * ((( 1 + (8*(fr_1**2)))**(1/2)) - 1), y_2 is calculated;
Using the Length of Hydraulic Jump on a Horizontal Floor Graph, fr_1 is calculated;
Using the following equation: corresponding_lb_y2 * y_2, l_b is calculated;
Using the following equation: ((l_t * (s_t - s0_income)) - (l_b * s0_income)) / (s_s + s0_income), l_s is calculated;
Using the following equation: (l_s * s_s) + z_1, z_3 is calculated.
Test whether tailwater is sufficient to force a jump in the basin.
If y_2 (Conjugate depth for the culvert outlet) + z_1 (Ground elevation at the basin entrance) < z_3 (Elevation at the entrance to the tailwater channel) + y_n_tw (Tail Water Depth (m)), tailwater is sufficient to force a jump in the basin;
If Tailwater is not sufficient, change the ground elevation at the basin entrance (m) (z_1) so that y_2 + z_1 > z_3 + y_n_tw.

### STEP 6
The needed Radius of curvature for the slope changes entering the Basin is determined.
Using the following equation: y_0 / ((math.exp(1.5 / (fr_0 ** 2))) - 1), r_slope is calculated.

### STEP 7
The Basin, Chute Blocks, Baffle Blocks and End Sill Dimension is determined.
Basin dimensions
Using the following equation: l_t + l_b + l_s, basin_length is calculated.
Chute Blocks dimensions
The height of chute blocks (h_1) is equal to Depth approaching the jump (y_1);
Using the following equation: math.ceil(w_b / (2*h_1)), the number of Chute Blocks is calculated;
Using the following equation: w_b / (2*n_c), number of Chute Block width & spacing is calculated;
Using the following equation: n_c - 1, the number of spaces between the Chute Blocks is calculated;
Using the following equation: w_b - ((n_c*block_w) + (chute_n_s*block_s)), the space width of the remaining spaces is calculated.
Baffle Blocks dimensions
​The height of chute blocks (h_1) is equal to the Depth approaching the jump (y_1);
Using the following equation: h_1 * ((0.168*fr_1) + 0.58), the height of the Baffle Blocks is calculated;
Using the following equation: math.ceil(w_b / (2*h_3)), the number of the Baffle Blocks is calculated;
Using the following equation: w_b / (2*n_b), the Baffle Block width and Baffle Block spacing are calculated;
Using the following equation: n_b - 1, the number of spaces between the Baffle Blocks is calculated;
Using the following equation:  w_b - ((n_b*baffle_w) + (baffle_n_s*baffle_s)), the remaining spaces is calculated;
Using the following equation:  0.8 * y_2, the distance from the downstream face of the chute blocks to the upstream face of the baffle block is calculated.
End Sill dimensions
Using the following equation:  h_1 * ((0.0536*fr_1) + 1.04), the height of the end sill is calculated.​

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## USBR Type IV Stilling Basin
Example of USBR Type IV Stilling Basin Dimensions: 
Froude Number - 2.5 (min), 4.5 (max) | Required Tailwater^3, m/ft - 3.5/11.2 | Basin Length, m/ft - 38.1/121.8 | Basin Depth, m/ft - 5.5/17.4

A USBR Type IV Stilling Basin is a specialized hydraulic structure developed by the United States Bureau of Reclamation for managing water flow from dams. This basin is designed to dissipate the energy of rapidly flowing water, preventing erosion and maintaining downstream stability. Unlike Type III, Type IV stilling basins incorporate additional features, such as stepped blocks and deflectors, to further break up the water's energy. The arrangement of these structures minimizes turbulence and promotes efficient energy dissipation. USBR Type IV Stilling Basins play a vital role in safeguarding riverbanks and channels, ensuring controlled water release while preventing damage to surrounding environments.

### USER INPUT
 - Discharge (cms);
 - Channel Width (B) (m) of Income Channel;
 - Longitudinal Slope (So) (m/m) of Income Channel;
 - Manning's Roughness (n) of Income Channel;
 - Ratio of tailwater to conjugate depth (TW/y2);
 - Ground elevation at the Incoming channel outlet (m);
 - Width of the basin (m/s);
 - Slope leaving the basin (m/m);
 - Slope of the transition entering the basin (m/m);
 - Longitudinal Slope (So) (m/m) of Outgoing Channel;
 - Mannings Roughness (n) of Outgoing Channel;
 - Channel Width (B) (m) of Outgoing Channel.

### STEP 1
Incoming Channel Brink Depth (y_0), Velocity (v_0) and Froude Number (fr_0) are determined.
Using the following equation: Q = (1/n) * ((A**(5/3)) / (P**(2/3))) * (S0**(1/2)), y_0 is calculated;
Using the following equation: Q / b*y, v_0 is calculated;
Using the following equation: v_0 / (sqrt(9.8*y_0)), fr_0 is calculated.

### STEP 2
Velocity (v_n) and Tail Water Depth (y_n_tw) in the receiving Channel Downstream of the Basin are determined.
Using the following equation: Q = (1/n) * ((A**(5/3)) / (P**(2/3))) * (S0**(1/2)), y_n_tw is calculated;
Using the following equation: Q / b*y, v_n is calculated.

### STEP 3
The Conjugate Depth for the income Channel Outlet Conditions is determined.
Using the following equation: ((c_income * y_0) / 2) * ((( 1 + (8*(fr_0**2)))**(1/2)) - 1), y_2_1 is calculated.
If y_2_1 > y_n_tw:
If y_2_1 ({y_2_1}) > TW ({y_n_tw}) a jump WILL NOT form and a basin is needed;
The process of Calculating Stilling Basin Dimensions will be continued below.
If y_2_1 <= y_n_tw:
Since y2 ({y_2_1}) <= TW ({y_n_tw}) a jump WILL form and a basin IS NOT needed.

### STEP 4
The length of the basin width is confirmed within acceptable limits.
Using the following equation: z_0 - (y_2_1 - y_n_tw), z_1 is calculated;
Using the following equation: (z_0 - z_1) / s_t, l_t is calculated.
Test: WB IS or IS NOT within acceptable limits:
Define test_wb as w_b + (((2*l_t) * (((s_t**2) + 1)**(1/2))) / (3 * fr_0));
If the Basin Width (w_b) is smaller (<) than or equal (=) to the test_wb, WB is within acceptable limits.
Using the following equation: Q = y_1 * w_b * ((((2 * 9.8) * (z_0 - z_1 + y_0 - y_1 )) + v_0²) ** (1/2)), y_1 is calculated;
Using the following equation: v_1 = Q / A, where A = y_1 * w_b, v_1 is calculated;
Using the following equation: (v_1) / ((9.8 * y_1)**(1/2)), fr_1 is calculated.

### STEP 5
Basin length and exit elevation are computed. Verify that sufficient tailwater exists to force the hydraulic jump.
Using the following equation: ((c_income * y_1) / 2) * ((( 1 + (8*(fr_1**2)))**(1/2)) - 1), y_2 is calculated;
Using the Length of Hydraulic Jump on a Horizontal Floor Graph, fr_1 is calculated;
Using the following equation: corresponding_lb_y2 * y_2, l_b is calculated;
Using the following equation: ((l_t * (s_t - s0_income)) - (l_b * s0_income)) / (s_s + s0_income), l_s is calculated;
Using the following equation: (l_s * s_s) + z_1, z_3 is calculated.
Test whether tailwater is sufficient to force a jump in the basin.
If y_2 (Conjugate depth for the culvert outlet) + z_1 (Ground elevation at the basin entrance) < z_3 (Elevation at the entrance to the tailwater channel) + y_n_tw (Tail Water Depth (m)), tailwater is sufficient to force a jump in the basin;
If Tailwater is not sufficient, change the ground elevation at the basin entrance (m) (z_1) so that y_2 + z_1 > z_3 + y_n_tw.

### STEP 6
The needed Radius of curvature for the slope changes entering the Basin is determined.
Using the following equation: y_0 / ((math.exp(1.5 / (fr_0 ** 2))) - 1), r_slope is calculated.

### STEP 7
The Basin, Chute Blocks and End Sill Dimension is determined.
Basin dimensions
Using the following equation: l_t + l_b + l_s, basin_length is calculated.
Chute Blocks dimensions
Using the following equation: 2 * y_1, the height of the Chute Blocks is calculated;
Using the following equation: math.ceil(w_b / (2.625*y_1)), number of Chute Blocks has been calculated;
Using the following equation: w_b / (3.5*n_c), number of Chute Block width is calculated;
Using the following equation: 2.5 * block_w, number of Chute Block spacing is calculated;
Using the following equation: n_c - 1, the number of spaces between the Chute Blocks is calculated;
Using the following equation: w_b - ((n_c*block_w) + (chute_n_s*block_s)), the space width of the remaining spaces is calculated.
End Sill dimensions
Using the following equation:  y_1 * ((0.0536*fr_1) + 1.04), the height of the end sill is calculated.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Saint Anthony Falls (SAF) Stilling Basin
Example of SAF Stilling Basin Dimensions:
Froude Number - 1.7 (min), 17 (max) | Required Tailwater^3, m/ft - 2.4/7.9 | Basin Length, m/ft - 12.4/39.7 | Basin Depth, m/ft - 2.7/8.6

The SAF (Stepped Apron with Flaps) Stilling Basin is an advanced hydraulic structure designed to dissipate the energy of rapidly flowing water, commonly used in dam projects. It features a stepped concrete apron with adjustable flaps or gates strategically placed along the steps. As water cascades down the steps, the flaps control the flow and dissipate energy, minimizing erosion and turbulence downstream. The stepped configuration and adjustable flaps allow for precise regulation of water velocity, ensuring efficient energy dissipation. SAF Stilling Basins are engineered to enhance safety, prevent erosion, and maintain the stability of riverbeds and banks while managing water release from dams.

### USER INPUT
 - Discharge (cms);
 - Channel Width (B) (m) of Income Channel;
 - Longitudinal Slope (So) (m/m) of Income Channel;
 - Manning's Roughness (n) of Income Channel;
 - Ratio of tailwater to conjugate depth (TW/y2);
 - Ground elevation at the Incoming channel outlet (m);
 - Width of the basin (m/s);
 - Slope leaving the basin (m/m);
 - Slope of the transition entering the basin (m/m);
 - Longitudinal Slope (So) (m/m) of Outgoing Channel;
 - Mannings Roughness (n) of Outgoing Channel;
 - Channel Width (B) (m) of Outgoing Channel.

### STEP 1
Incoming Channel Brink Depth (y_0), Velocity (v_0) and Froude Number (fr_0) are determined.
Using the following equation: Q = (1/n) * ((A**(5/3)) / (P**(2/3))) * (S0**(1/2)), y_0 is calculated;
Using the following equation: Q / b*y, v_0 is calculated;
Using the following equation: v_0 / (sqrt(9.8*y_0)), fr_0 is calculated.

### STEP 2
Velocity (v_n) and Tail Water Depth (y_n_tw) in the receiving Channel Downstream of the Basin are determined.
Using the following equation: Q = (1/n) * ((A**(5/3)) / (P**(2/3))) * (S0**(1/2)), y_n_tw is calculated;
Using the following equation: Q / b*y, v_n is calculated.

### STEP 3
The Conjugate Depth for the income Channel Outlet Conditions is determined.
Using the following equation: ((c_income * y_0) / 2) * ((( 1 + (8*(fr_0**2)))**(1/2)) - 1), y_2_1 is calculated.
If y_2_1 > y_n_tw:
If y_2_1 ({y_2_1}) > TW ({y_n_tw}) a jump WILL NOT form and a basin is needed;
The process of Calculating Stilling Basin Dimensions will be continued below.
If y_2_1 <= y_n_tw:
Since y2 ({y_2_1}) <= TW ({y_n_tw}) a jump WILL form and a basin IS NOT needed.

### STEP 4
The length of the basin width is confirmed within acceptable limits.
Using the following equation: z_0 - (y_2_1 - y_n_tw), z_1 is calculated;
Using the following equation: (z_0 - z_1) / s_t, l_t is calculated.
Test: WB IS or IS NOT within acceptable limits:
Define test_wb as w_b + (((2*l_t) * (((s_t**2) + 1)**(1/2))) / (3 * fr_0));
If the Basin Width (w_b) is smaller (<) than or equal (=) to the test_wb, WB is within acceptable limits.
Using the following equation: Q = y_1 * w_b * ((((2 * 9.8) * (z_0 - z_1 + y_0 - y_1 )) + v_0²) ** (1/2)), y_1 is calculated;
Using the following equation: v_1 = Q / A, where A = y_1 * w_b, v_1 is calculated;
Using the following equation: (v_1) / ((9.8 * y_1)**(1/2)), fr_1 is calculated.

### STEP 5
Basin length and exit elevation are computed. Verify that sufficient tailwater exists to force the hydraulic jump.
Using the following equation: ((c_income * y_1) / 2) * ((( 1 + (8*(fr_1**2)))**(1/2)) - 1), y_2 is calculated;
Using the Length of Hydraulic Jump on a Horizontal Floor Graph, fr_1 is calculated;
Using the following equation: corresponding_lb_y2 * y_2, l_b is calculated;
Using the following equation: ((l_t * (s_t - s0_income)) - (l_b * s0_income)) / (s_s + s0_income), l_s is calculated;
Using the following equation: (l_s * s_s) + z_1, z_3 is calculated.
Test whether tailwater is sufficient to force a jump in the basin.
If y_2 (Conjugate depth for the culvert outlet) + z_1 (Ground elevation at the basin entrance) < z_3 (Elevation at the entrance to the tailwater channel) + y_n_tw (Tail Water Depth (m)), tailwater is sufficient to force a jump in the basin;
If Tailwater is not sufficient, change the ground elevation at the basin entrance (m) (z_1) so that y_2 + z_1 > z_3 + y_n_tw.

### STEP 6
The needed Radius of curvature for the slope changes entering the Basin is determined.
Using the following equation: y_0 / ((math.exp(1.5 / (fr_0 ** 2))) - 1), r_slope is calculated.

### STEP 7
The Basin, Chute Blocks, Baffle Blocks and End Sill Dimension is determined.
Basin dimensions
Using the following equation: l_t + l_b + l_s, basin_length is calculated.
Chute Blocks dimensions
The height of chute blocks (h_1) is equal to Depth approaching the jump (y_1);
Using the following equation: math.ceil(w_b / (1.5*y_1)), number of Chute Blocks is calculated;
Using the following equation: w_b / (2*n_c), number of Chute Block width & spacing is calculated;
Using the following equation: n_c - 1, the number of spaces between the Chute Blocks is calculated;
Using the following equation: w_b - ((n_c*block_w) + (chute_n_s*block_s)), the space width of the remaining spaces is calculated;
Baffle Blocks dimensions
The height of Baffle Blocks (h_3) is equal to Depth approaching the jump (y_1);​
Using the following equation: math.ceil(w_b / (1.5*y_1)), the number of the Baffle Blocks is calculated;
Using the following equation: w_b / (2*n_b), the Baffle Block width and Baffle Block spacing are calculated;
Using the following equation: n_b - 1, the number of spaces between the Baffle Blocks is calculated;
Using the following equation:  w_b - ((n_b*baffle_w) + (baffle_n_s*baffle_s)), the remaining spaces is calculated;
Using the following equation:  ((n_b * baffle_w) / w_b)*100, the percentage blocked by baffles is calculated;
Using the following equation:  l_b/3, the distance from the downstream face of the chute blocks to the upstream face of the baffle block is calculated.
End Sill dimensions
Using the following equation:  (0.07 * y_2) / c_income, the height of the end sill is calculated.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Straight Drop Structure
A Straight Drop Structure is a hydraulic engineering feature designed to facilitate the controlled vertical discharge of water from a higher elevation to a lower one. It is often used in various water management systems, such as spillways in dams, stormwater management, and irrigation channels. The structure typically consists of a vertical chute or channel with a constant slope, allowing water to descend smoothly without abrupt changes in direction.

​Key components of a Straight Drop Structure include an entrance section, a vertical drop section, and an exit section. The entrance section directs the incoming flow into the vertical drop, where the water experiences a significant energy loss due to the sudden change in elevation. This energy dissipation helps prevent erosion downstream and minimizes turbulence.

Straight Drop Structures are versatile and can be customized to suit specific flow rates and site conditions. They are essential in maintaining the integrity of hydraulic systems by efficiently managing water discharge and preventing erosion, particularly in situations where steep gradients or rapid flow changes are involved.

### USER INPUT
 - Discharge (cms);
 - Vertical drop between approach and TW channel;
 - Spillway notch length (m);
 - Width of rectangular outgoing channel barrel (m);
 - Slope of the bed (m/m);
 - Manning's Roughness (n) of Outgoing Channel.

### STEP 1
The elevation difference required between the approach and tailwater channel, h (m), is estimated by user.
User estimated the required approach and tailwater channel elevation difference, h;
This drop forces the slope of the upstream and downstream channel to s_0 (Slope of the bed (m/m), as also given by the user.

### STEP 2
Normal depth in the tailwater channel (y_0), Velocity of flow in the tailwater channel (v_0) and approaching channel Froude Number (fr_0) are determined.
Using the following equation: Q = (1/n) * ((A**(5/3)) / (P**(2/3))) * (S0**(1/2)), y_0 is calculated;
Using the following equation: q_discharge_cms / (b_out * y_0), v_0 is calculated;
Using the following equation: v_0 / (math.sqrt(9.8*y_0)), fr_0 is calculated;
The state of Flow is determined.

### STEP 3
The Critical Depth is calculated over the weir (usually rectangular) into the drop structure. The vertical dimensions of the stilling basin are also calculated.
Using the following equation: q_discharge_cms / b_out, q is calculated;
Using the following equation: (q**2 / 9.8)**(1/3), y_c is calculated;
Using the following equation: 2.15 * y_c, y_3 is calculated;
Using the following equation: - (h - y_0), h_2 is calculated;
Using the following equation: h_2 - y_3, h_0 is calculated;
Using the following equation: - 1 * (h_0 + h), depression is calculated.

### STEP 4
Estimate the basin length.
Using the following equation: ((-0.406) + (3.195 - (4.368 * (h_0 / y_c))) ** (1/2)) * y_c, l_f is calculated;
Using the following equation: (-0.406 + (3.195 - 4.368 * (h_2 / y_c)) ** (1/2)) * y_c, l_t is calculated;
Using the following equation: ((0.691 + (0.228 * ((l_t / y_c) ** 2)) - (h_0 / y_c)) * y_c ) / ( 0.185 + 0.456 * (l_t / y_c)), l_s is calculated;
Using the following equation: (l_f + l_s) / 2, l_1 is calculated;
Using the following equation: 0.8 * y_c, l_2 is calculated;
Using the following equation: 1.75 * y_c, l_3 is calculated.

### STEP 5
Design the basin floor blocks and end sill.
Using the following equation: 0.85 * y_c, sidewall_height is calculated;
Using the following equation: 0.4 * y_c, b_w is calculated;
Using the following equation: 0.4 * y_c, end_sill_height is calculated.

### STEP 6
Design the basin exit and entrance transitions.
Using the following equation: 0.85 * y_c, sidewall_height is calculated;
Using the following equation: 3 * y_c, armour_approach is calculated.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------
