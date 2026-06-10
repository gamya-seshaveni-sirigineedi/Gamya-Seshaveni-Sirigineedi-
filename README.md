const projects = [
    {
        name: "Retail Sales Analysis",
        description: "Analyzed sales data using Python."
    },
    {
        name: "Plantation Drive Project",
        description: "Studied impact of plantation drives on local temperature."
    }
];

let output = "";
projects.forEach(project => {
    output += `<h3>${project.name}</h3><p>${project.description}</p>`;
});

document.getElementById("projects").innerHTML = output;
