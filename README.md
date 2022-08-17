# SQL
SQL portfolio
Welcome to my SQL portfolio! This code repository contains examples of SQL I've written. Feel free to take a look and reach out if you have any questions

-- Working with Covid Data

-- Select Data that we are going to use

Select location, date, total_cases, new_cases, total_deaths, population from portfolioproject..CovidDeaths order by 1,2

--Finding Total Cases vs Total Deaths --Shows likelihood of dying of covid if you contract the virus in diffirect countries

Select location, date, total_cases, total_deaths,(Total_deaths/ total_cases)*100 as Deathpercentage from portfolioproject..CovidDeaths Wher location like '%states%' order by 1,2

--Looking at Total Cases vs Population --Shows what percentage of population got Covid

Select location, date, total_cases, population, (total_cases/Population)*100 as PercentagePopulationInfected from portfolioproject..CovidDeaths Where location like '%states%' order by 1,2

--Looking at Countries with Highest infection Rate compared to Population

Select location, population MAX(total_cases) as HighestInfectionCount, MAX(total_cases/Population))*100 as PercentagePopulationInfected from portfolioproject..CovidDeaths Where location like '%states%' Group by Location, Population Order by PercentagePopulationInfected desc

--Showing Countries with Highest Death Count per Population

Select location, MAX(total_deaths) as TotalDeathCount From portfolioproject..CovidDeaths Where location like '%states%' Where continent is not null Group by Location Order by TotalDeathCount desc

--Showing Total Cases Globally vs Total Deaths

Select date, Sum(new_cases),Sum (new_deaths) total_deaths,(Total_deaths/ total_cases)*100 as Deathpercentage from portfolioproject..CovidDeaths Where location like '%states Where continent is not null

Select SUM (new cases) as total cases, SUM(new deaths) as total deaths, SUM(new deaths)/SUM(New Cases)*100 as DeathPercentage From PortfolioProject..CovidDeaths -Where location like "%states%' where continent is not null --Group By date order by 1,2

--Looking at Total Population vs Vaccinations

Select dea.continent, dea.location, dea.date, dea.populatian, vac.new_vaccinations
, SUM(CONVERT (int, vac. new_vaccinations)) OVER (Partition by dea. Location Order by dea.location, dea.Date) as RollingPeopleVaccinated
-, (RollingPeopleVaccinated/population)*100
From PortfolioProject….CovidDeaths dea
Join PortfolioProject..CovidVaccinationsvac
On dea.location = vac.location
and dea.date = vac.date
where dea. continent is not null
order by 2,3

--Creating View to store data for later visualizations

Create View PercentPopulationVacciated as
Select dea.continent, dea.location, dea.date, dea.population, vac.new_vaccinations
, SUM(CONVERT (int, vac.new_vaccinations)) OVER (Partition by dea. Location Order by dea.location, dea.Date) as RollingPeopleVaccinated
(RollingPeopleVaccinated/population)*100
From PortfolioProject..CovidDeaths dea
Join PortfolioProject..CovidVaccinationsvac
On dea.location = vac.location
and dea.date = vac.date
where dea. continent is not null
--order by 2,3

Select
From PercentPopulationVaccinated
