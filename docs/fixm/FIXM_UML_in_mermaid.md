# FIXM UML in Mermaid

## Address 1

```mermaid
classDiagram
class ContactInformation
ContactInformation : TextName [0..1]+name
ContactInformation : ContactInformationExtension [0..2000]+extension
%% ContactInformation : PostalAddress [0..1]+address
%% ContactInformation : OnlineContact [0..2000]+onlineContact
%% ContactInformation : TelephoneContact [0..1]+phoneFax
ContactInformation : TextName [0..1]+title
class TelephoneContact
TelephoneContact : TelephoneContactExtension [0..2000]+extension
TelephoneContact : TextPhone [0..1]+facsimile
TelephoneContact : TextPhone [0..1]+voice
class PostalAddress
PostalAddress : TextName [0..1]+administrativeArea
PostalAddress : PostalAddressExtension [0..2000]+extension
PostalAddress : TextCity [0..1]+city
PostalAddress : TextCountryCode [0..1]+countryCode
PostalAddress : TextCountryName [0..1]+countryName
PostalAddress : TextAddress [0..1]+deliveryPoint
PostalAddress : TextName [0..1]+postalCode
class OnlineContact
OnlineContact : OnlineContactExtension [0..2000]+extension
OnlineContact : TextAddress [0..1]+email
OnlineContact : TextAddress [0..1]+linkage
%% OnlineContact : NetworkChoice [0..1]+network
class NetworkChoice
<<choice>> NetworkChoice
NetworkChoice : CharacterString +other
%% NetworkChoice : TelecomNetworkType +type
class TelecomNetworkType{
<<enumeration>>
AFTN
INTERNET
}
ContactInformation --> "0..1" TelephoneContact : +phoneFax
ContactInformation --> "0..1" PostalAddress : +address
ContactInformation --> "0..1" OnlineContact : +onlineContact
OnlineContact --> "0..1" NetworkChoice : +network
NetworkChoice --> TelecomNetworkType : +type
```

## AeronauticalReference

### SignificantPoint

```mermaid
classDiagram
class SignificantPointChoiceType
<<choice>> SignificantPointChoiceType
%% SignificantPointChoiceType : AerodromeReferenceType [1..1]+aerodromeReferencePoint
%% SignificantPointChoiceType : DesignatedPointType [1..1]+designatedPoint
%% SignificantPointChoiceType : NavaidType [1..1]+navaid
%% SignificantPointChoiceType : GeographicalPositionType [1..1]+position
%% SignificantPointChoiceType : RelativePointType [1..1]+relativePoint
class DesignatedPointType
DesignatedPointType : DesignatedPointExtensionType [0..2000]+extension
DesignatedPointType : HypertextReferenceType [0..1]+href
DesignatedPointType : DesignatedPointDesignatorType [1..1]+designator
%% DesignatedPointType : GeographicalPositionType [0..1]+position
class NavaidType
NavaidType : NavaidExtensionType [0..2000]+extension
NavaidType : NavaidDesignatorType [1..1]+designator
NavaidType : HypertextReferenceType [0..1]+href
NavaidType : NavaidServiceTypeType [0..1]+navaidServiceType
%% NavaidType : GeographicalPositionType [0..1]+position
class RelativePointType
RelativePointType : BearingType [1..1]+bearing
RelativePointType : DistanceType [1..1]+distance
RelativePointType : RelativePointExtensionType [0..2000]+extension
%% RelativePointType : GeographicalPositionType [0..1]+position
%% RelativePointType : NavaidType [1..1]+referencePoint
class GeographicalPositionType
GeographicalPositionType : LatLongPosType [1..1]+pos
%% GeographicalPositionType : urn:ogc:def:crs:EPSG::4326 srsName
GeographicalPositionType : GeographicalPositionExtensionType [0..2000]+extension
class AerodromeReferenceType
AerodromeReferenceType : AerodromeReferenceExtensionType [0..2000]+extension
AerodromeReferenceType : IataAerodromeDesignatorType [0..1]+iataDesignator
AerodromeReferenceType : LocationIndicatorType [0..1]+locationIndicator
AerodromeReferenceType : AerodromeNameType [0..1]+name
%% AerodromeReferenceType : GeographicalPositionType [0..1]+referencePoint
AerodromeReferenceType : HypertextReferenceType [0..1]+href
SignificantPointChoiceType --> AerodromeReferenceType : +aerodromeReferencePoint
SignificantPointChoiceType --> DesignatedPointType : +designatedPoint
SignificantPointChoiceType --> NavaidType : +navaid
SignificantPointChoiceType --> GeographicalPositionType : +position
SignificantPointChoiceType --> RelativePointType : +relativePoint
DesignatedPointType --> "0..1" GeographicalPositionType : +position
NavaidType --> "0..1" GeographicalPositionType : +position
RelativePointType --> "0..1" GeographicalPositionType : +position
RelativePointType --> NavaidType : +referencePoint
AerodromeReferenceType --> "0..1" GeographicalPositionType : +referencePoint
```