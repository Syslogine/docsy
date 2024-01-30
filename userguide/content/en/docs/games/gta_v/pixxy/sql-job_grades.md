---
linktitle: "SQL job_grades"
---


```sql
INSERT INTO `job_grades` (`id`, `job_name`, `grade`, `name`, `label`, `salary`, `skin_male`, `skin_female`) VALUES
    (27, 'ambulance', 0, 'jremt', 'Jr. EMT', 25, '{}', '{}'),
    (28, 'ambulance', 1, 'emt', 'EMT', 50, '{}', '{}'),
    (29, 'ambulance', 2, 'sr_emt', 'Sr. EMT', 75, '{}', '{}'),
    (30, 'ambulance', 3, 'emt_supervisor', 'EMT Supervisor', 100, '{}', '{}'),
    (31, 'ambulance', 4, 'chief_emt', 'Chief EMT', 125, '{}', '{}'),
    (32, 'ambulance', 5, 'ambulance_supervisor', 'Ambulance Supervisor', 150, '{}', '{}'),
    (33, 'ambulance', 6, 'ambulance_manager', 'Ambulance Manager', 175, '{}', '{}');

INSERT INTO `job_grades` (`id`, `job_name`, `grade`, `name`, `label`, `salary`, `skin_male`, `skin_female`) VALUES
	(36, 'banker', 0, 'consultant', 'Consultant', 10, '{}', '{}'),
	(37, 'banker', 1, 'banker', 'Banker', 20, '{}', '{}'),
	(38, 'banker', 2, 'business_banker', 'Investment Banker', 30, '{}', '{}'),
	(39, 'banker', 3, 'trader', 'Broker', 40, '{}', '{}'),
	(40, 'banker', 4, 'bank_manager', 'Bank Manager', 50, '{}', '{}'),
	(41, 'banker', 5, 'bank_director', 'Bank Director', 60, '{}', '{}'),
	(42, 'banker', 6, 'bank_executive', 'Bank Executive', 70, '{}', '{}');

INSERT INTO `job_grades` (`id`, `job_name`, `grade`, `name`, `label`, `salary`, `skin_male`, `skin_female`) VALUES
	(43, 'bartender', 0, 'barback', 'Barback', 10, '{}', '{}'),
	(44, 'bartender', 1, 'apprentice_bartender', 'Apprentice Bartender', 20, '{}', '{}'),
	(45, 'bartender', 2, 'mixologist', 'Mixologist', 30, '{}', '{}'),
	(46, 'bartender', 3, 'senior_bartender', 'Senior Bartender', 40, '{}', '{}'),
	(47, 'bartender', 4, 'bar_manager', 'Bar Manager', 50, '{}', '{}'),
	(48, 'bartender', 5, 'nightclub_owner', 'Nightclub Owner', 60, '{}', '{}'),
	(49, 'bartender', 6, 'cocktail_mogul', 'Cocktail Mogul', 70, '{}', '{}');

INSERT INTO `job_grades` (`id`, `job_name`, `grade`, `name`, `label`, `salary`, `skin_male`, `skin_female`) VALUES
	(50, 'bountyhunter', 0, 'trainee_hunter', 'Trainee Hunter', 20, '{}', '{}'),
	(51, 'bountyhunter', 1, 'licensed_hunter', 'Licensed Hunter', 40, '{}', '{}'),
	(52, 'bountyhunter', 2, 'experienced_hunter', 'Experienced Hunter', 60, '{}', '{}'),
	(53, 'bountyhunter', 3, 'master_hunter', 'Master Hunter', 80, '{}', '{}'),
	(54, 'bountyhunter', 4, 'bounty_hunter_chief', 'Bounty Hunter Chief', 100, '{}', '{}'),
	(55, 'bountyhunter', 5, 'bounty_hunter_guild_leader', 'Bounty Hunter Guild Leader', 120, '{}', '{}'),
	(56, 'bountyhunter', 6, 'legendary_bounty_hunter', 'Legendary Bounty Hunter', 140, '{}', '{}');

INSERT INTO `job_grades` (`id`, `job_name`, `grade`, `name`, `label`, `salary`, `skin_male`, `skin_female`) VALUES
	(57, 'busdriver', 0, 'novice_driver', 'Novice Driver', 15, '{}', '{}'),
	(58, 'busdriver', 1, 'experienced_driver', 'Experienced Driver', 30, '{}', '{}'),
	(59, 'busdriver', 2, 'route_supervisor', 'Route Supervisor', 45, '{}', '{}'),
	(60, 'busdriver', 3, 'fleet_manager', 'Fleet Manager', 60, '{}', '{}'),
	(61, 'busdriver', 4, 'transportation_director', 'Transportation Director', 75, '{}', '{}'),
	(62, 'busdriver', 5, 'public_transit_executive', 'Public Transit Executive', 90, '{}', '{}'),
	(63, 'busdriver', 6, 'city_transport_commissioner', 'City Transport Commissioner', 105, '{}', '{}');

INSERT INTO `job_grades` (`id`, `job_name`, `grade`, `name`, `label`, `salary`, `skin_male`, `skin_female`) VALUES
	(64, 'cardealer', 0, 'sales_trainee', 'Sales Trainee', 20, '{}', '{}'),
	(65, 'cardealer', 1, 'sales_associate', 'Sales Associate', 40, '{}', '{}'),
	(66, 'cardealer', 2, 'experienced_salesperson', 'Experienced Salesperson', 60, '{}', '{}'),
	(67, 'cardealer', 3, 'sales_manager', 'Sales Manager', 80, '{}', '{}'),
	(68, 'cardealer', 4, 'luxury_car_specialist', 'Luxury Car Specialist', 100, '{}', '{}'),
	(69, 'cardealer', 5, 'dealership_director', 'Dealership Director', 120, '{}', '{}'),
	(70, 'cardealer', 6, 'automotive_tycoon', 'Automotive Tycoon', 140, '{}', '{}');

INSERT INTO `job_grades` (`id`, `job_name`, `grade`, `name`, `label`, `salary`, `skin_male`, `skin_female`) VALUES
	(71, 'casinodealer', 0, 'trainee_dealer', 'Trainee Dealer', 20, '{}', '{}'),
	(72, 'casinodealer', 1, 'card_shark', 'Card Shark', 40, '{}', '{}'),
	(73, 'casinodealer', 2, 'roulette_pro', 'Roulette Pro', 60, '{}', '{}'),
	(74, 'casinodealer', 3, 'poker_master', 'Poker Master', 80, '{}', '{}'),
	(75, 'casinodealer', 4, 'blackjack_kingpin', 'Blackjack Kingpin', 100, '{}', '{}'),
	(76, 'casinodealer', 5, 'casino_supervisor', 'Casino Supervisor', 120, '{}', '{}'),
	(77, 'casinodealer', 6, 'casino_manager', 'Casino Manager', 140, '{}', '{}');

INSERT INTO `job_grades` (`id`, `job_name`, `grade`, `name`, `label`, `salary`, `skin_male`, `skin_female`) VALUES
	(78, 'deliverydriver', 0, 'trainee_driver', 'Trainee Driver', 15, '{}', '{}'),
	(79, 'deliverydriver', 1, 'local_courier', 'Local Courier', 30, '{}', '{}'),
	(80, 'deliverydriver', 2, 'express_delivery_specialist', 'Express Delivery Specialist', 45, '{}', '{}'),
	(81, 'deliverydriver', 3, 'fleet_supervisor', 'Fleet Supervisor', 60, '{}', '{}'),
	(82, 'deliverydriver', 4, 'logistics_manager', 'Logistics Manager', 75, '{}', '{}'),
	(83, 'deliverydriver', 5, 'courier_captain', 'Courier Captain', 90, '{}', '{}'),
	(84, 'deliverydriver', 6, 'delivery_mogul', 'Delivery Mogul', 110, '{}', '{}');

INSERT INTO `job_grades` (`id`, `job_name`, `grade`, `name`, `label`, `salary`, `skin_male`, `skin_female`) VALUES
	(85, 'dj', 0, 'amateur_dj', 'Amateur DJ', 30, '{}', '{}'),
	(86, 'dj', 1, 'party_mixer', 'Party Mixer', 50, '{}', '{}'),
	(87, 'dj', 2, 'club_dj', 'Club DJ', 80, '{}', '{}'),
	(88, 'dj', 3, 'radio_host', 'Radio Host', 100, '{}', '{}'),
	(89, 'dj', 4, 'festival_headliner', 'Festival Headliner', 150, '{}', '{}'),
	(90, 'dj', 5, 'music_producer', 'Music Producer', 200, '{}', '{}'),
	(91, 'dj', 6, 'dj_superstar', 'DJ Superstar', 250, '{}', '{}');

INSERT INTO `job_grades` (`id`, `job_name`, `grade`, `name`, `label`, `salary`, `skin_male`, `skin_female`) VALUES
	(92, 'drug_dealer', 0, 'street_peddler', 'Street Peddler', 50, '{}', '{}'),
	(93, 'drug_dealer', 1, 'small_time_dealer', 'Small-Time Dealer', 100, '{}', '{}'),
	(94, 'drug_dealer', 2, 'drug_kingpin', 'Drug Kingpin', 200, '{}', '{}'),
	(95, 'drug_dealer', 3, 'narcotics_syndicate', 'Narcotics Syndicate', 350, '{}', '{}'),
	(96, 'drug_dealer', 4, 'cartel_leader', 'Cartel Leader', 500, '{}', '{}'),
	(97, 'drug_dealer', 5, 'underground_chemist', 'Underground Chemist', 750, '{}', '{}'),
	(98, 'drug_dealer', 6, 'drug_lord', 'Drug Lord', 1000, '{}', '{}');

INSERT INTO `job_grades` (`id`, `job_name`, `grade`, `name`, `label`, `salary`, `skin_male`, `skin_female`) VALUES
    (99, 'fisherman', 0, 'beginner_angler', 'Beginner Angler', 25, '{}', '{}'),
    (100, 'fisherman', 1, 'amateur_fisher', 'Amateur Fisher', 50, '{}', '{}'),
    (101, 'fisherman', 2, 'experienced_fisherman', 'Experienced Fisherman', 75, '{}', '{}'),
    (102, 'fisherman', 3, 'professional_angler', 'Professional Angler', 100, '{}', '{}'),
    (103, 'fisherman', 4, 'fishing_captain', 'Fishing Captain', 125, '{}', '{}'),
    (104, 'fisherman', 5, 'master_angler', 'Master Angler', 150, '{}', '{}'),
    (105, 'fisherman', 6, 'legendary_fisher', 'Legendary Fisher', 175, '{}', '{}');

INSERT INTO `job_grades` (`id`, `job_name`, `grade`, `name`, `label`, `salary`, `skin_male`, `skin_female`) VALUES
	(106, 'flight_instructor', 0, 'trainee_pilot', 'Trainee Pilot', 20, '{}', '{}'),
	(107, 'flight_instructor', 1, 'novice_aviator', 'Novice Aviator', 40, '{}', '{}'),
	(108, 'flight_instructor', 2, 'certified_instructor', 'Certified Instructor', 60, '{}', '{}'),
	(109, 'flight_instructor', 3, 'flight_specialist', 'Flight Specialist', 100, '{}', '{}'),
	(110, 'flight_instructor', 4, 'chief_flight_instructor', 'Chief Flight Instructor', 150, '{}', '{}'),
	(111, 'flight_instructor', 5, 'aviation_mentor', 'Aviation Mentor', 200, '{}', '{}'),
	(112, 'flight_instructor', 6, 'flight_school_director', 'Flight School Director', 300, '{}', '{}');

INSERT INTO `job_grades` (`id`, `job_name`, `grade`, `name`, `label`, `salary`, `skin_male`, `skin_female`) VALUES
	(113, 'fueler_truck', 0, 'fueling_assistant', 'Fueling Assistant', 12, '{}', '{}'),
	(114, 'fueler_truck', 1, 'fuel_technician', 'Fuel Technician', 18, '{}', '{}'),
	(115, 'fueler_truck', 2, 'diesel_mechanic', 'Diesel Mechanic', 25, '{}', '{}'),
	(116, 'fueler_truck', 3, 'fleet_supervisor', 'Fleet Supervisor', 35, '{}', '{}'),
	(117, 'fueler_truck', 4, 'fueling_manager', 'Fueling Manager', 45, '{}', '{}'),
	(118, 'fueler_truck', 5, 'transportation_fuel_specialist', 'Transportation Fuel Specialist', 55, '{}', '{}'),
	(119, 'fueler_truck', 6, 'chief_fuel_officer', 'Chief Fuel Officer', 70, '{}', '{}');

INSERT INTO `job_grades` (`id`, `job_name`, `grade`, `name`, `label`, `salary`, `skin_male`, `skin_female`) VALUES
    (120, 'lumberjack', 0, 'lumberjack_trainee', 'Lumberjack Trainee', 30, '{}', '{}'),
    (121, 'lumberjack', 1, 'woodcutter', 'Woodcutter', 45, '{}', '{}'),
    (122, 'lumberjack', 2, 'forestry_technician', 'Forestry Technician', 60, '{}', '{}'),
    (123, 'lumberjack', 3, 'timber_specialist', 'Timber Specialist', 75, '{}', '{}'),
    (124, 'lumberjack', 4, 'lumberyard_supervisor', 'Lumberyard Supervisor', 90, '{}', '{}'),
    (125, 'lumberjack', 5, 'forest_manager', 'Forest Manager', 110, '{}', '{}'),
    (126, 'lumberjack', 6, 'lumber_baron', 'Lumber Baron', 130, '{}', '{}');

INSERT INTO `job_grades` (`id`, `job_name`, `grade`, `name`, `label`, `salary`, `skin_male`, `skin_female`) VALUES
    (127, 'news_anchor', 0, 'news_intern', 'News Intern', 20, '{}', '{}'),
    (128, 'news_anchor', 1, 'junior_reporter', 'Junior Reporter', 40, '{}', '{}'),
    (129, 'news_anchor', 2, 'senior_correspondent', 'Senior Correspondent', 60, '{}', '{}'),
    (130, 'news_anchor', 3, 'news_anchor', 'News Anchor', 80, '{}', '{}'),
    (131, 'news_anchor', 4, 'lead_anchor', 'Lead Anchor', 100, '{}', '{}'),
    (132, 'news_anchor', 5, 'news_director', 'News Director', 120, '{}', '{}'),
    (133, 'news_anchor', 6, 'network_executive', 'Network Executive', 140, '{}', '{}');

INSERT INTO `job_grades` (`id`, `job_name`, `grade`, `name`, `label`, `salary`, `skin_male`, `skin_female`) VALUES
    (134, 'mechanic', 0, 'recruit', 'Recruit', 25, '{}', '{}'),
    (135, 'mechanic', 1, 'novice', 'Novice', 50, '{}', '{}'),
    (136, 'mechanic', 2, 'experienced', 'Experienced', 75, '{}', '{}'),
    (137, 'mechanic', 3, 'leader', 'Leader', 100, '{}', '{}'),
    (138, 'mechanic', 4, 'boss', 'Boss', 125, '{}', '{}'),
    (139, 'mechanic', 5, 'master_mechanic', 'Master Mechanic', 150, '{}', '{}'),
    (140, 'mechanic', 6, 'engine_whisperer', 'Engine Whisperer', 175, '{}', '{}');

INSERT INTO `job_grades` (`id`, `job_name`, `grade`, `name`, `label`, `salary`, `skin_male`, `skin_female`) VALUES
    (141, 'miner', 0, 'employee', 'Employee', 25, '{}', '{}'),
    (142, 'miner', 1, 'laborer', 'Laborer', 50, '{}', '{}'),
    (143, 'miner', 2, 'digger', 'Digger', 75, '{}', '{}'),
    (144, 'miner', 3, 'foreman', 'Foreman', 100, '{}', '{}'),
    (145, 'miner', 4, 'mining_engineer', 'Mining Engineer', 125, '{}', '{}'),
    (146, 'miner', 5, 'mine_owner', 'Mine Owner', 150, '{}', '{}'),
    (147, 'miner', 6, 'mineral_magnate', 'Mineral Magnate', 175, '{}', '{}');

INSERT INTO `job_grades` (`id`, `job_name`, `grade`, `name`, `label`, `salary`, `skin_male`, `skin_female`) VALUES
    (148, 'police', 0, 'recruit', 'Recruit', 20, '{}', '{}'),
    (149, 'police', 1, 'officer', 'Officer', 40, '{}', '{}'),
    (150, 'police', 2, 'sergeant', 'Sergeant', 60, '{}', '{}'),
    (151, 'police', 3, 'lieutenant', 'Lieutenant', 85, '{}', '{}'),
    (152, 'police', 4, 'captain', 'Captain', 100, '{}', '{}'),
    (153, 'police', 5, 'chief', 'Chief', 150, '{}', '{}'),
    (154, 'police', 6, 'police_commissioner', 'Police Commissioner', 200, '{}', '{}');

INSERT INTO `job_grades` (`id`, `job_name`, `grade`, `name`, `label`, `salary`, `skin_male`, `skin_female`) VALUES
    (155, 'reporter', 0, 'employee', 'Employee', 0, '{}', '{}'),
    (156, 'reporter', 1, 'junior_reporter', 'Junior Reporter', 15, '{}', '{}'),
    (157, 'reporter', 2, 'senior_reporter', 'Senior Reporter', 30, '{}', '{}'),
    (158, 'reporter', 3, 'editor', 'Editor', 45, '{}', '{}'),
    (159, 'reporter', 4, 'chief_editor', 'Chief Editor', 75, '{}', '{}'),
    (160, 'reporter', 5, 'news_director', 'News Director', 100, '{}', '{}'),
    (161, 'reporter', 6, 'media_mogul', 'Media Mogul', 150, '{}', '{}');

INSERT INTO `job_grades` (`id`, `job_name`, `grade`, `name`, `label`, `salary`, `skin_male`, `skin_female`) VALUES
    (162, 'slaughterer', 0, 'employee', 'Employee', 0, '{}', '{}'),
    (163, 'slaughterer', 1, 'butcher', 'Butcher', 10, '{}', '{}'),
    (164, 'slaughterer', 2, 'meat_cutter', 'Meat Cutter', 20, '{}', '{}'),
    (165, 'slaughterer', 3, 'inventory_manager', 'Inventory Manager', 30, '{}', '{}'),
    (166, 'slaughterer', 4, 'shop_owner', 'Shop Owner', 45, '{}', '{}'),
    (167, 'slaughterer', 5, 'master_butcher', 'Master Butcher', 60, '{}', '{}'),
    (168, 'slaughterer', 6, 'meat_mogul', 'Meat Mogul', 80, '{}', '{}');

INSERT INTO `job_grades` (`id`, `job_name`, `grade`, `name`, `label`, `salary`, `skin_male`, `skin_female`) VALUES
    (169, 'tailor', 0, 'employee', 'Employee', 0, '{}', '{}'),
    (170, 'tailor', 1, 'seamstress', 'Seamstress', 10, '{}', '{}'),
    (171, 'tailor', 1, 'seamster', 'Seamster', 10, '{}', '{}'),
    (172, 'tailor', 2, 'fashion_designer', 'Fashion Designer', 20, '{}', '{}'),
    (173, 'tailor', 3, 'bespoke_tailor', 'Bespoke Tailor', 30, '{}', '{}'),
    (174, 'tailor', 4, 'fashion_boutique_owner', 'Fashion Boutique Owner', 45, '{}', '{}'),
    (175, 'tailor', 5, 'couturier', 'Couturier', 60, '{}', '{}'),
    (176, 'tailor', 6, 'fashion_magnate', 'Fashion Magnate', 80, '{}', '{}');

INSERT INTO `job_grades` (`id`, `job_name`, `grade`, `name`, `label`, `salary`, `skin_male`, `skin_female`) VALUES
    (177, 'taxi', 0, 'recruit', 'Recruit', 12, '{}', '{}'),
    (178, 'taxi', 1, 'novice', 'Novice', 24, '{}', '{}'),
    (179, 'taxi', 2, 'experienced', 'Experienced', 36, '{}', '{}'),
    (180, 'taxi', 3, 'uber_cabby', 'Uber Cabby', 48, '{}', '{}'),
    (181, 'taxi', 4, 'lead_cabby', 'Lead Cabby', 60, '{}', '{}');

INSERT INTO `job_grades` (`id`, `job_name`, `grade`, `name`, `label`, `salary`, `skin_male`, `skin_female`) VALUES
    (182, 'unemployed', 1, 'job_seeker', 'Job Seeker', 5, '{}', '{}'),
    (183, 'unemployed', 2, 'freelancer', 'Freelancer', 10, '{}', '{}'),
    (184, 'unemployed', 3, 'self_employed', 'Self-Employed', 15, '{}', '{}'),
    (185, 'unemployed', 4, 'small_business_owner', 'Small Business Owner', 25, '{}', '{}'),
    (186, 'unemployed', 5, 'entrepreneur', 'Entrepreneur', 35, '{}', '{}'),
    (187, 'unemployed', 6, 'business_magnate', 'Business Magnate', 50, '{}', '{}'),
    (188, 'unemployed', 7, 'tycoon', 'Tycoon', 100, '{}', '{}'),
    (189, 'unemployed', 8, 'unemployed_mogul', 'Unemployed Mogul', 200, '{}', '{}'),
    (190, 'unemployed', 9, 'server_owner', 'Server Owner', 500, '{}', '{}'),
    (191, 'unemployed', 10, 'grandmaster', 'Grandmaster', 1000, '{}', '{}'),
    (192, 'unemployed', 11, 'server_developer', 'Server Developer', 2000, '{}', '{}'),
    (193, 'unemployed', 12, 'coder', 'Coder', 3000, '{}', '{}'),
    (194, 'unemployed', 13, 'scripting_god', 'Scripting God', 5000, '{}', '{}'),
    (195, 'unemployed', 14, 'ai_programmer', 'AI Programmer', 10000, '{}', '{}');

```