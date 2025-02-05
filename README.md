# AR-VR-Enabled-Platform-for-Educational-Institutions
In today’s digital age, advanced technologies such as Augmented Reality (AR) and Mixed Reality (MR) have become powerful tools that significantly enhance user experiences across various fields. From education to investment and entertainment, these technologies play a vital role in improving understanding and interaction with surrounding environments by blending digital elements with the real world. Our project aims to leverage these cutting-edge technologies to create an innovative AR-based navigation solution tailored specifically to support educational institutions but also adaptable to various other environments. Our goal is to provide an interactive, user-friendly experience that makes it easier for users to navigate large and complex spaces, such as campuses, using smartphones or mobile devices.
Our project responds to the growing need for modern technology in improving the efficiency of educational institutions. We are working on developing a navigation system based on augmented reality to guide students and visitors within academic institutions using real-time data and interactive maps. This project, which is currently being tested at the Faculty of Engineering at Helwan University, relies on technologies such as 3D scanning using LiDAR sensors, along with the integration of university systems’ data to provide a personalized and unique experience for each user.

1.1 Challenges and Solutions
Many educational institutions face challenges in guiding students and visitors through large and complex spaces, especially when institutions are spread over multiple buildings or floors. Traditional solutions such as paper maps or signage may be ineffective and insufficient to meet the needs of modern users who increasingly rely on smartphones. Therefore, our project comes as an innovative solution that uses AR technology to offer interactive maps, updated data, and visual and audio cues that help users easily reach their destinations.

In this project, we use 3D scanning to create precise models of real-world environments within the campus, enabling us to seamlessly and effectively integrate AR elements. Through mixed reality technology, users can interact with digital elements integrated into their real-world environment, such as seeing live directions through their phone’s camera to reach a specific destination or interacting with informative details about buildings and locations within the university.

1.2 The Role of Cloud Technology
A key feature of our project is utilizing cloud infrastructure for secure data transmission and storage, allowing users to access live maps and information at anytime from anywhere. The 3D models created using LiDAR sensors are uploaded to a cloud database, where they are processed and integrated with location data and navigation instructions within the app. This cloud platform offers great scalability, allowing the solution to be implemented in multiple institutions and different spaces without needing to reconfigure the system entirely.
We are also working on providing a flexible solution that enables deployment through local servers if needed, offering certain institutions more control over their data and privacy. This approach enhances security and ensures the protection of users’ personal data in sensitive environments like universities or government institutions.

1.3 Application at Helwan University
As a practical example, our team is currently conducting a case study at the Faculty of Engineering at Helwan University to develop a virtual environment accessible via mobile devices. Users scan QR codes with their smartphone cameras to receive instant guidance and directions. The system integrates with the university’s database, providing additional features such as lecture schedules, virtual attendance at events, and real-time direction details.

The solution is designed to be adaptable to other environments and institutions, making it a comprehensive solution that can be customized to meet the needs of various institutions. The system is based on an interactive user interface designed to be user-friendly, even for those with no advanced technical experience. It also includes advanced features such as location sharing and live chat, providing a comprehensive and interactive educational experience.

lidar sensor in iphone 14 pro - we take 5 shots of 3D scanning of Departmer's build. 
and we improve the 3D scanning and integrate the all layers in one shot to export it to unity editor.
Using ![WhatsApp Image 2025-02-05 at 10 10 31 AM (1)](https://github.com/user-attachments/assets/41cb5e22-3451-442c-9bcd-74e1003f7089)

![WhatsApp Image 2025-02-05 at 10 10 30 AM (2)](https://github.com/user-attachments/assets/54c5648e-b50e-4577-8737-fda1447f41a4)


![WhatsApp Image 2025-02-05 at 10 10 31 AM (2)](https://github.com/user-attachments/assets/ad541b09-a91c-4673-8f06-567d433791c0)

![WhatsApp Image 2025-02-05 at 10 10 31 AM](https://github.com/user-attachments/assets/4e19056e-7d33-4320-9e67-80b4a71389aa)

![WhatsApp Image 20![WhatsApp Image 2025-02-05 at 10 10 30 AM (1)](https://github.com/user-attachments/assets/dc5882ca-1557-403d-9f9e-cb8d809f0e52)
25-02-05 at 10 10 30 AM (3)](https://github.com/user-attachments/assets/5392aa84-fec3-4bf0-85e2-464d53328f0a)

![WhatsApp Image 2025-02-05 at 10 10 30 AM](https://github.com/user-attachments/assets/887f867f-d85c-401c-a456-d286b67a52a7)



In Unity editor i started making navigation system with refrences point marker .. and started writing c# code files to run the navigation line - some of important tools which i use in unity for my AR app 
1- AR foundation. 
2- AR ratcasting.
3- AI navigation.
4- AR Kit for building ios app 
5- plane detection.
![image](https://github.com/user-attachments/assets/7b674e53-2465-41da-956f-317ca5fad05b)


DestinationSelector code

using UnityEngine;
using UnityEngine.UI;

public class DestinationSelector : MonoBehaviour
{
    public Transform[] destinations;
    public NavigationController navigator; 

    
    public void SelectDestination(int index)
    {
        navigator.SetDestination(destinations[index]); 
    }
}

UserLocationTracker code 

using UnityEngine;
using UnityEngine.XR.ARFoundation;
using UnityEngine.XR.ARSubsystems;
using System.Collections.Generic;

public class UserLocationTracker : MonoBehaviour
{
    public ARRaycastManager raycastManager;
    public Transform userMarker;  
    private List<ARRaycastHit> hits = new List<ARRaycastHit>();

    void Update()
    {
        // Raycast 
        Vector2 screenCenter = new Vector2(Screen.width / 2, Screen.height / 2);
        if (raycastManager.Raycast(screenCenter, hits, TrackableType.Planes))
        {
            Pose hitPose = hits[0].pose;
            userMarker.position = hitPose.position;  
        }
    }
}


NavigationController code

using UnityEngine;

public class NavigationController : MonoBehaviour
{
    public Transform player; 
    public LineRenderer lineRenderer; 

 
    public void SetDestination(Transform target)
    {
        DrawPath(player.position, target.position); 
    }

   
    private void DrawPath(Vector3 start, Vector3 end)
    {
        lineRenderer.positionCount = 2; 
        lineRenderer.SetPosition(0, start); 
        lineRenderer.SetPosition(1, end);   

        lineRenderer.startWidth = 0.1f; 
        lineRenderer.endWidth = 0.1f;   
        lineRenderer.material.color = Color.green; 
    }
}



